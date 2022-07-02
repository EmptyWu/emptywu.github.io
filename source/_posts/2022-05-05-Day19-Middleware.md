---
layout: post
title: Day19-Middleware
tags: [Express,Node.js,JavaScript]
author: EmptyWu
date: 2022-05-07 02:36:03
category: Node.js
description: Express 在收到 request 到回傳 response，中間會經過一系列的 middleware（中間件/中介軟體）處理，
---

## 前言
Express 在收到 request 到回傳 response，中間會經過一系列的 middleware（中間件/中介軟體）處理， 
middleware 本身像是一個守門員的概念，通常會使用 app.use((req, res, next) => {...}) 並帶入 function，function 中除了 req 及 res 參數，還有 next，當執行 next() 就代表要將控制權交給下一個 Middleware
需注意若在 Middleware 最後沒有執行 next()，程式就會停留在這個 Middleware，無法進入下一個階段

<!--more-->

使用 app.use((req, res, next) => {...}) 的寫法在接收 request 時都會經過此 middleware，若是只想要在接收特定 request 時經過 middleware 把關，也可以改為此寫法
```javascript
const checkLogin = (req,res,next) => {
    const url = req.url;
    if(url !== '/'){
        next()
    } else {
      res.send('你的登入資料有錯！')
    }
}
// 將 middleware 放在特定的路由中，只有接收到此 request 才會經過 checkLogin middleware
app.get('/', checkLogin, function(req,res){
  res.send('<html><head></head><body><h1>Login</h1></body></html>')
})
```

### 參考資源

[使用 Express 中介軟體](https://expressjs.com/zh-tw/guide/using-middleware.html)
[middleware 設計](https://courses.hexschool.com/courses/1670869/lectures/39299787)（章節影片）

## 練習
使用 `app.use()` 設計一個處理錯誤路由以及一個伺服器程式錯誤的 Middleware，

- 處理錯誤路由：
當 client 端造訪錯誤的路由，就回傳狀態碼 404，並回傳 JSON 物件，status 為 `'error'`，回饋訊息 message 為`無此頁面資訊`

```
const errorRoute =function (req, res, next){
  res.status(404).send(
    {
      status: 'error',
      message: '無此頁面資訊'
    }
  );
}
app.use((errorRoute);
```

- 伺服器程式錯誤：
當 server 端有程式出錯的情況，導致 client 端無法正確造訪路由，就回傳狀態碼 500，並回傳 JSON 物件，status 為 `'error'`，回饋訊息 message 為 `系統錯誤，請恰系統管理員`

```
app.use((err,req,res,next)=>{
    res.status(500).send({
        status:'error',
        message:'系統錯誤，請恰系統管理員',
        stack: err.stack
    })
})
```
以上見解，如有錯誤地方還請留言告知，感謝。