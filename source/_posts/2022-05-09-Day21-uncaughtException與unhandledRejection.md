---
layout: post
title: Day21-uncaughtException與unhandledRejection
tags: [Express,Node.js,JavaScript]
author: EmptyWu
date: 2022-05-10 20:23:38
category: Node.js
description: 在設計程式時也有可能會有開發者程式沒寫好、沒考慮到的部分，這時可能就因此出現不可預期的錯誤，因此在 Node.js，運行程式出錯時，若是同步的程式就會出現 uncaughtException，非同步程式則會出現 unhandledRejection
---

## 前言
在設計程式時也有可能會有開發者程式沒寫好、沒考慮到的部分，這時可能就因此出現不可預期的錯誤，因此在 Node.js，運行程式出錯時，若是同步的程式就會出現 uncaughtException，非同步程式則會出現 unhandledRejection

同步的錯誤例如：app.js 中有出現未宣告過的變數 test
非同步錯誤例如：某 async function 中，未使用到 await，或遠端資料庫連線失敗 （若未使用 catch 接錯誤就會發生 unhandledRejection）

在事件發生時，將錯誤記錄於 server，並在處理後離開此 process


<!--more-->
## uncaughtException 處理範例
```javascript
// 程式出現重大錯誤時
process.on('uncaughtException', err => {
  // 記錄錯誤下來，等到服務都處理完後，停掉該 process
	console.error('Uncaughted Exception！')
	console.error(err);
	process.exit(1);
});
```
出錯時的紀錄會出現:
```javascript
Uncaughted Exception！
ReferenceError: test is not defined
    at Object.<anonymous> (...略)
```
**uncaughtException 處理範例**
```javascript
// 未捕捉到的 catch 
process.on('unhandledRejection', (reason, promise) => {
  console.error('未捕捉到的 rejection：', promise, '原因：', reason);
  // 記錄於 log 上
});
```
出錯時的紀錄會出現
```javascript
未捕捉到的 rejection： Promise {
  <rejected> ReferenceError: timeSor is not defined
      at ...略
} 原因： ReferenceError: timeSor is not defined
    at ...略
```

### 參考資源

[Event: uncaughtException](https://nodejs.org/api/process.html#event-uncaughtexception)
[Event: unhandledrejection](https://nodejs.org/api/process.html#event-unhandledrejection)

以上見解，如有錯誤地方還請留言告知，感謝。