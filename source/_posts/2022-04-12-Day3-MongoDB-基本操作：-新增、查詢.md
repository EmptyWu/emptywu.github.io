---
layout: post
title: Day3-MongoDB 基本操作： 新增、查詢
tags: [MongoDB,insert,query]
author: EmptyWu
date: 2022-04-12 23:16:25
category: 資料庫
description: MongoDB是一個NoSQL資料庫，以文件(document)導向的資料庫管理系統，比起傳統的資料庫，非關聯式特性在處理巨量資料的時候可以更快。
---

## 前言

MongoDB是一個NoSQL資料庫，以文件(document)導向的資料庫管理系統，比起傳統的資料庫，非關聯式特性在處理巨量資料的時候可以更快。

MongoDB 會以 **BSON** 的形式儲存資料（Binary JSON），相較於 JSON 儲存的資料類型更多。

整體資料結構為：db -> collection -> document
我們可以透過指令（The mongo Shell）的方式用終端機來操作資料庫

<!--more-->

## 新增
### 新增單筆
```javascript
db.collection.insertOne(
   {
    example: "ex1"
   }
)
```

### 新增多筆
```javascript
db.collection.insertMany(
   {
    example: "ex1"
   },
   {
    example: "ex2"
   }
   ...
)
```

## 查詢
```javascript
db.collection.find({})
```
直接查詢collection 的資料全部列出
若要查詢特定的資料在 `find()` 帶入 `{ 屬性： 值 }` 尋找符合的條件的資料

可使用 **比較運算式** 設定篩選條件

| $eq  | 等於         |
| ---- | ------------ |
| $ne  | 不等於       |
| $gt  | 大於         |
| $lt  | 小於         |
| $gte | 大於等於     |
| $lte | 小於等於     |
| $in  | 存在某個值   |
| $nin | 不存在某個值 |

可使用以下 **邏輯運算式**

| $and | 全部條件皆符合 |
| ---- | -----------  |
| $or  | 符合其中一項條件|
| $nor | 全部條件皆不符合|
| $not | 與條件相反    |

例：找出collection 中符合以下條件之一的資料:class屬性為A或score 小於60

```javascript
db.collection.find({ $or: [ { class: "A" }, { score: { $lt: 60 } } ] })
```

使用**正歸表達式** 選有符合的文字
```javascript
db.collection.find({ example: /text/})
```

建立一個 database（名稱可自定義），並建立一個 students collection
```json
  {
    "studentName": "Riley Parker",
    "group": "A",
    "score": 83,
    "isPaid": false
  }
```
範例：
```javascript
db.students.insertOne({
    "studentName": "Riley Parker",
    "group": "A",
    "score": 83,
    "isPaid": false
})
```

2. 依以下格式一次新增多筆 document 到 `students` collection
```json
db.students.insertMany(
{
  "studentName": "Brennan Miles",
  "group": "C",
  "score": 72,
  "isPaid": false
},
{
  "studentName": "Mia Diaz",
  "group": "B",
  "score": 98,
  "isPaid": true
},
{
  "studentName": "Caroline morris",
  "group": "B",
  "score": 55,
  "isPaid": false
},
{
  "studentName": "Beverly Stewart",
  "group": "B",
  "score": 60,
  "isPaid": false
}
)
```

3. 查詢 `students` collection 中的所有資料
```json
db.students.find()
```
4. 查詢 `students` collection 中符合 group 屬性為 B 的資料 `使用 { <field>: <value> } 設定符合的項目`
```json
db.students.find({"group":"b"})
```
5. 查詢 `students` collection 中符合分數在 60 分以上的的資料
```json
db.students.find({"score":{"$gte":60}})
```
6. 查詢 `students` collection 中符合分數在 60 分以下**或是** group 為 B 的資料
```json
db.students.find({$or: ["score":{"$lte":60},{"group":"b"}]})
```


以上見解，如有錯誤地方還請留言告知，感謝。