---
layout: post
title: Day17-Mongoose-Populate
tags: [Mongoose,Schema,MongoDB,JavaScript]
author: EmptyWu
date: 2022-05-07 02:20:44
category: 資料庫
description: Mongoose 有提供 populate() 方法，可以將其他 collection 的資料關聯到目前在操作的 collection
---

## 前言

Mongoose 有提供 populate() 方法，可以將其他 collection 的資料關聯到目前在操作的 collection

<!--more-->
這裡引用官方文件中的範例
```javascript
const mongoose = require('mongoose');
const { Schema } = mongoose;

const personSchema = Schema({
  _id: Schema.Types.ObjectId,
  name: String,
  age: Number,
  stories: [{ type: Schema.Types.ObjectId, ref: 'Story' }]
});

const storySchema = Schema({
  author: { type: Schema.Types.ObjectId, ref: 'Person' },
  title: String,
  fans: [{ type: Schema.Types.ObjectId, ref: 'Person' }]
});

const Story = mongoose.model('Story', storySchema);
const Person = mongoose.model('Person', personSchema);
```
可以看到上方最後兩行有兩個 Model，分別是 Story 和 Person，兩者也都有連到各自的資料庫 collection
personSchema 中的 `stories` 欄位關聯至 storySchema 的 `id` 欄位，storySchema 的 `author` 及 `fans` 欄位，其中 `ref` 選項是告訴 Mongoose 關聯資料時要使用哪個 Model

接下來取得資料時就可以使用 `populate()` 加入相關設定，就可以在取得資料時依據 Schema 的設定取得其他 collection 的資料
```javascript
Story.
  find().
  populate({ path: 'fans', select: 'name' })
```
取得 Story 資料時，資料的 fans 欄位就會關聯至 Person collection，找出符合該 id 的 document，`select` 是指定要取出該 document 的哪些欄位，上方範例是取出 document 中的 `name` 欄位
取出多個欄位的寫法為 `select: 'name age'`，就會取出 document 中的 `name` 和 `age` 欄位


## 參考資源

[Mongoose v6.3.1: Query Population](https://mongoosejs.com/docs/populate.html)

## 練習
以下為書籍與作者的 collection，請填入對應答案，讓取出單筆書籍資料時，可以關聯至 author 的資料

```javascript
const mongoose = require('mongoose');

const authorSchema = new mongoose.Schema({
    name: String,
    introduction: String
  }, { versionKey: false }
);
// models/books.js
const bookSchema = new mongoose.Schema({
  author : { type: mongoose.Schema.ObjectId, ref: Author },
  title: String
}, { versionKey: false }
);

const Author = mongoose.model('Author', authorSchema);
const Book = mongoose.model('Book', bookSchema);
```
取出所有 books 的資料，關聯 author 欄位並指定顯示 author 資料的 name 欄位
```javascript
Book.find({_id: id }).populate({path: 'author', select: 'name'})
```

以上見解，如有錯誤地方還請留言告知，感謝。