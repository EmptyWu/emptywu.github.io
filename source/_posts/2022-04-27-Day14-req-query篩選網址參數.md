---
layout: post
title: Day14-req.query篩選網址參數
tags: [Express,Node.js,JavaScript]
author: EmptyWu
date: 2022-05-07 01:57:59
category: Node.js
description: 先前使用 `req.params` 取得動態路由外，也可在 url 帶入相關資訊，再使用 `req.query` 取出網址列的參數
---


## 前言
先前使用 `req.params` 取得動態路由外，也可在 url 帶入相關資訊，再使用 `req.query` 取出網址列的參數
<!--more-->

例如：網址列為 `https://example.com/over/there?name=ferrett&color=purple`，其中 ? 用來分隔後面帶入的參數 `name=ferret` 及 `color=purple`，多個參數之間也會使用 & 分隔

當使用者造訪此網址時， express 可以使用 req.query 取出網址列的這些參數 
```javascript
app.get('https://example.com/over/there?name=ferrett&color=purple)', function(req, res) {
  console.log(req.query)
  ...
});

// req.query
{ 
  name: 'ferret',
  color: 'purple'
}
```
使用 `req.query.name` 或 `req.query.color` 就可以取出需要的資訊做相關處理

req.query 常見的應用是搜尋關鍵字，當使用者輸入關鍵字後，會將關鍵字帶到網址列中，伺服器接收到，再藉由 req.query 取出，尋找資料庫中符合其關鍵字的資料，並回傳至客戶端

```
GET 'https://example.com/search?q=apple' // 通常會以 q 表示搜尋關鍵字
```
```javascript
app.get('/search', function(req, res) {
  const q = req.query.q
  const results = await Data.find(q); // 使用 mongoose 搜尋資料庫中符合 req.query.q 的資料
  res.status(200).json({
    status: 'success',
    results: results.length,
    data: {
        results
    }
  });
});
```


## 參考資源

[Express - req.query](https://expressjs.com/zh-tw/api.html#req.query)
[query - 取得網址參數](https://courses.hexschool.com/courses/1670869/lectures/39299606)（章節影片）

## 練習

以下 url 中的參數使用 req.query 取出，並回傳取出的參數
```javascript
'http://localhost:3000/products?category=music&page=1' // 在 POSTMAN 發出 GET 請求
app.get('/products', function(req, res) {
  // 取出參數
  const { category, page } = req.query;
  res.status(200).json({
    status: 'success',
    data: {
        category,
        page
    }
  });
});
```

以上見解，如有錯誤地方還請留言告知，感謝。