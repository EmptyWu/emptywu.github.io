---
layout: post
title: Day2-非同步概念、使用 Promise
tags: [JavaScript,Promise]
author: EmptyWu
date: 2022-04-11 22:12:43
category: JavaScript
description: Promise 是一個物件，代表一個即將完成或失敗的非同步操作，以及回傳的值
---

## 前言

Promise 是一個物件，代表一個即將完成或失敗的非同步操作，以及回傳的值

<!--more-->

## Promise 寫法
```Javascript
function example() {
  new Promise((resolve, reject) => {
  // 執行一些非同步作業，最終呼叫:
  //
  // resolve(someValue); // 實現
  // 或
  // reject("failure reason"); // 拒絕
  } )
}
```
建立好 Promise 後，執行此函式就可以在完成 Promise 時使用 .then() 接收回傳的 Promise 物件，以及使用 .catch() 接收錯誤，
因 Promise 可以用鍊式寫法接收上一個 Promise 的回傳值，不需像使用 callback function 一層包一層，因此可以提昇易讀性。

```Javascript
example()
  .then(data => 
    useData(data)
  )
  .catch(error =>
    console.log(error)
  )
```

## 實際做法
```Javascript
// 批改作業
function correctTest(name) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const score = Math.round(Math.random()*100);
      if(score >= 60) {
        resolve({
          name,
          score
        })
      } else {
        reject("您已達退學門檻")
      }
    }, 2000)
  })
}
// 檢查獎勵
function checkReward(data) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if(data.score >= 90) {
        resolve(`${data.name} 獲得電影票`);
      } else if (data.score >= 60 && data.score < 90) {
        resolve(`${data.name} 獲得嘉獎`);
      } else {
        reject(`您沒有獎品`)
      }
    }, 2000)
  })
}
// 執行函式
correctTest('EmptpyWu')
 .then(data => checkReward(data))
 .then(result => console.log(result))
 .catch((error)=>{
     console.log(error);
 });
```

以上見解，如有錯誤地方還請留言告知，感謝。