---
layout: post
title: Day5-非同步概念、async await
tags: [JavaScript,async,await]
author: EmptyWu
date: 2022-04-15 08:54:34
category: JavaScript
description: async 及 await 是非同步函式的一種寫法，可以讓非同步的執行更趨近於同步作業。
---

## 前言
async 及 await 是非同步函式的一種寫法，可以讓非同步的執行更趨近於同步作業。
在非同步函式前加上 async，此函式時回傳值就會被轉為一個 Promise。

在 async 非同步函式中，使用 await 等待接收回傳的結果，因此會暫停此函式的執行，並且等待 Promise 的解析，解析完回傳值，並繼續下一個 async 函式的執行。

也就是說在未等待回傳結果，不會執行下一個程式

例：
```javascript
function resolveAfter2Seconds(x) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}


async function add1(x) {
  const a = await resolveAfter2Seconds(20);
  const b = await resolveAfter2Seconds(30);
  return x + a + b;
}
```
<!--more-->

## 練習

流程：
批改作業 → 檢查獎勵 → 給予獎勵 → 退學或懲罰
```javascript
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
```
將以下這段程式碼改寫為 async await 的寫法
```javascript
const init = async function() {
 await correctTest("Empty")
 .then(source=>await checkReward(source))
 .then(reward=> console.log(reward))
 .catch((err)=>console.log(err))
 ;
}
init();
```

以上見解，如有錯誤地方還請留言告知，感謝。