---
layout: post
title: Day18-取得資料搭配 sort()、limit()
tags: [Mongoose,Schema,MongoDB,JavaScript]
author: EmptyWu
date: 2022-05-07 02:30:05
category: 資料庫
description: Mongoose 的 sort() 可使用物件寫法
---

## 前言
Mongoose 的 sort() 可使用物件寫法

<!--more-->
```
sort({ field: 'asc', test: -1 }) 
// field 欄位以升序排列，test 欄位以降序排列
```
，也可只帶入欄位名稱（欄位名稱前加上 - 代表降序排列）
```
query.sort('field -test');
// field 欄位以升序排列，test 欄位以降序排列
```

Mongoose 的 `limit()` 可直接帶入數字，如：`.limit(20)` 代表最多呈現 20 筆資料


## 參考資源

[Query.prototype.sort()](https://mongoosejs.com/docs/api/query.html#query_Query-sort)
[Query.prototype.limit()](https://mongoosejs.com/docs/api/query.html#query_Query-limit)

## 練習
運用 Express 提供的 req.query 取得網址列的參數，將尋找到符合的資料設定排序及呈現指定資料數量

提交範例
```javascript

// routes/posts.js

router.get('/', async function(req, res, next) {
  // 使用三元運算子判斷是否為 asc (由舊至新)，若是則由舊至新排列，否則由新至舊排列
  const timeSort = req.query.timeSort === 'asc' ? 'createAt' : '-createAt';
  // 帶入網址列的參數
  const limit = +req.query.limit;
  const post = await Post.find().sort(timeSort).limit(limit);/* 請填入答案 */
  res.status(200).json({
    status: 'success',
    data: {
      post
    }
  });
})
```

以上見解，如有錯誤地方還請留言告知，感謝。