---
layout: post
title: Day23-development 及 production 環境變數指令、客製錯誤訊息
tags: [Express,Node.js,javascript]
author: EmptyWu
date: 2022-05-10 22:41:13
category: Node.js
description: 由於通常不會將開發時遇到的詳細錯誤資訊（如 error.stack）呈現在客戶端，避免過多資訊暴露而有資安疑慮，因此會區分 development 及 production 模式下的錯誤訊息
---

## 前言
由於通常不會將開發時遇到的詳細錯誤資訊（如 error.stack）呈現在客戶端，避免過多資訊暴露而有資安疑慮，因此會區分 development 及 production 模式下的錯誤訊息

可在錯誤處理 (error handler) middleware 判斷 Node.js 環境變數
`process.env.NODE_ENV` 為 `dev` 或是 `production`（下方 error handler 範例 31 及 33 行），以提供不同錯誤處理

<!--more-->
:::spoiler error handler 範例
```javascript
// 自己設定的 err 錯誤 
const resErrorProd = (err, res) => {
  if (err.isOperational) {
    res.status(err.statusCode).json({
      status: err.status,
      message: err.message
    });
  } else {
    // log 紀錄
    console.error('出現重大錯誤', err);
    // 送出罐頭預設訊息
    res.status(500).json({
      status: 'error',
      message: '系統錯誤，請恰系統管理員'
    });
  }
};
// 開發環境錯誤
const resErrorDev = (err, res) => {
  res.status(err.statusCode).json({
    status: err.status,
    message: err.message,
    error: err,
    stack: err.stack
  });
};
// error handler
app.use(function(err, req, res, next) {
  err.statusCode = err.statusCode || 500;
  err.status = err.status || 'error';
  if (process.env.NODE_ENV === 'dev') {
    resErrorDev(err, res);
  } else if (process.env.NODE_ENV === 'production') {
    if(err.isAxiosError == true){
      err.message = "axios 連線錯誤";
      err.isOperational = true;
      return resErrorProd(err, res)
    } else if (err.name === 'ValidationError'){
      // mongoose 資料辨識錯誤
      err.isOperational = true;
      return resErrorProd(err, res)
    }
    resErrorProd(err, res)
  }
});
```
:::
範例中分別以 `resErrorDev(err, res)` `resErrorProd(err, res)` 回傳不同模式回饋錯誤的 JSON 資料
Production 模式會依據是否為預期 client 端可能會出現的錯誤，決定是否回傳提示 client 端錯誤處，若為 server 端需處理的錯誤，則回傳「系統錯誤，請恰系統管理員」的文字，不需回傳相關錯誤資訊

設定好不同模式的錯誤回饋後，在 package.json 設定設定執行指令，測試不同模式是否有正確回饋錯誤訊息
```javascript
"scripts": {
    "start:dev": "NODE_ENV=dev nodemon ./bin/www",
    "start:production": "NODE_ENV=production nodemon ./bin/www"
},
```
若是 windows 系統可能會遇到不支援執行以上指令的情況，可安裝 [cross-env 套件](https://www.npmjs.com/package/cross-env)
並調整為以下指令
```javascript
"scripts": {
    "start:dev": "cross-env NODE_ENV=dev nodemon ./bin/www",
    "start:production": "cross-env NODE_ENV=production nodemon ./bin/www"
},
```
 ## 參考資源
[GitHub 範例](https://github.com/gonsakon/express-week4-sample/blob/week5/app.js#L47-L86)

## 練習
error handler 範例，設計 POST 新增貼文時的 development 及 production 模式的錯誤處理，並以 POSTMAN 測試可正確運作

```json
// production 模式
{
    "status": 400,
    "message": "資料格式錯誤"
}

// devlopment 模式
{
    "status": 400,
    "message": "Unexpected end of JSON input",
    "error": {
        "expose": true,
        "statusCode": 400,
        "status": 400,
        "body": "{\n \"name\": \"test1\",\n \"content\": \"test1\",\n \"tags\": [\"感情\"],\n \"type\": \"person\"\n",
        "type": "entity.parse.failed"
    },
    "stack": "SyntaxError: Unexpected end of JSON input\n    at JSON.parse (<anonymous>)\n    ...略"
}
```
## 解答

```javascript
const express =require('express');
const app=express();
//開發錯誤
const developmentError=(err,res)=>{
    res.status(err.statusCode).Json({
        status:err.status,
        message:err.message,
        error:err,
        stack:err.stack
    })
}
//正式錯誤
const productionError = (err,res)=>{
    if(err.isOperational){
        res.status(err.statusCode).Json({
                status:err.status,
                message:err.message              
            })
    }else{
        console.log('系統發生錯誤',err);
        res.status(500).json({
            status:'error',
            message:'系統發生錯誤'
        })
    }
}

app.use((err, req, res, next) => {
    err.statusCode = err.statusCode || 500
    err.status = err.status || 'error'
     if (process.env.NODE_ENV === 'development') developmentError(err, res)
    // 正式環境
    if (process.env.NODE_ENV === 'production') {
        productionError(err, res)
    }
});
```


以上見解，如有錯誤地方還請留言告知，感謝。