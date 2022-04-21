---
layout: post
title: Day1-非同步概念、建立 Promise
tags: [JavaScript,Promise]
date: 2022-04-11 21:55:30
category: JavaScript
description: Promise 非同步作法，以往的非同步作法是使用callback function 寫法，這個寫法會一層一層下去比較難閱讀；而Promise是比較新的非同步作法，更容易閱讀一些 
author: EmptyWu
---

## 前言

Promise 非同步作法，以往的非同步作法是使用callback function 寫法，這個寫法會一層一層下去比較難閱讀；而Promise是比較新的非同步作法，更容易閱讀一些
<!--more-->

## 建立Promist 語法
```Javascript
new Promise((resolve, reject) => {
  // 執行一些非同步作業，最終呼叫:
  //
  // resolve(someValue); // 實現
  // 或
  // reject("failure reason"); // 拒絕
} );
```

其中兩個參數 resolve 及 reject 都是函式，分別代表實現(完成)及拒絕的函式，非同步成功就會執行resolve函式完成Promise；
失敗則執行reject 函式，執行reject 函式會回傳error物件或失敗訊息。


## 在原有funtion 中修改為 Promise

原本語法
```Javascript
const checkScore = (score) => {
  /* 回傳一個 Promise，並執行以下非同步操作*/
  const score = Math.round(Math.random() * 100);
  /* 判斷流程請嘗試使用 setTimeout() 執行 */
  if(score >= 60) {
    console.log(score); // 執行實現方法
  } else {
    console.log("不及格"); // 執行拒絕方法
  }
}
checkScore();
```
使用 Promise 語法改寫
```Javascript
const checkScore = (score)=>{
  return new Promise((res, rej)=>{
    const score = Math.round(Math.random() * 100);
    setTimeout(() => {
      if (score >= 60) {
        res(console.log(score)); // 執行實現方法
      } else {
        rej(console.log("不及格"));// 執行拒絕方法
      }
    }, 1000);
  }); 
};

checkScore();
```
其中增加了 promise ，且增加了setTimeout ，模擬非同地的等待


以上見解，如有錯誤地方還請留言告知，感謝。