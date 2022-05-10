---
layout: post
title: Day16-req.params取得特定資料
tags: [Express,Node.js,javascript]
author: EmptyWu
date: 2022-05-07 02:06:56
category: Node.js
description: 接續前面，請參考如下
---


## 前言
接續前面，請參考如下
<!--more-->

## 參考資源
[Express 4.x - API 參照(req.params)](https://expressjs.com/zh-tw/api.html#req.params)
[params - 取得指定路徑](https://courses.hexschool.com/courses/1670869/lectures/39299605)（章節影片）

## 練習

使用 express 提供的 req.params 取得貼文 id，並使用 mongoose 尋找符合 id 的資料，最後 response 該特定貼文資料（若 id 不存在可做簡易錯誤處理）
```javascript
const express = require('express');
const router = express.Router();
const Post = require('../models/posts');

router.get('/:id', async(req, res, next) =>  {
  try {
      const id = req.params?.id;
      const post = Post.findById(id)
      if(post == null || id == null) {
          res.status(400).json({
              status: 'false',
              message: 'id 錯誤'
          });
      } else {
          res.status(200).json({
              status: 'success',
              message: post
          });
      }
  } catch (error) {
    res.status(400).json({
        status: 'false',
        message: error.message
    });
  }
})
```

以上見解，如有錯誤地方還請留言告知，感謝。