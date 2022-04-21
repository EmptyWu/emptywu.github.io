---
layout: post
title: Day4-MongoDB 基本操作： 修改、刪除
tags: [MongoDB,update,delete]
author: EmptyWu
date: 2022-04-14 08:48:38
category: 資料庫
description: MongoDB是一個NoSQL資料庫，以文件(document)導向的資料庫管理系統，比起傳統的資料庫，非關聯式特性在處理巨量資料的時候可以更快。
---

## 前言
繼上一篇新增、刪除後，這邊來說明修改、刪除Monhodb部分。


<!--more-->

## 修改
### 修改單筆資料
`updateOne()` 
1. 第一個參數：透過設定符合的屬性找出要修改的資料，
若第一個參數帶入空物件 {}，則會選取全部資料的第一筆資料
2. 第二個參數放入要修改的屬性，需先加上 $set 物件，並在此物件中帶入要修改的物件屬性。
第二個參數可選擇帶入 $currentDate 屬性，修改資料後顯示修改時間。

```Javascript
db.collection.updateOne(
   {
    example: "text"
   },
   {
    $set: {
      example: "texttext"
    },
    $currentDate: {
      lastModified: true
    }
   }
)
```

### 修改多筆資料
```Javascript
db.collection.updateMany(
   {
    example: /text/
   },
   {
    $set: {
      example: "texttext"
    },
    $currentDate: {
      lastModified: true
    }
   }
)
```

## 刪除
### 刪除單筆資料
```Javascript
db.collection.deleteOne(
   {
    example: /text/
   } 
)
```

### 刪除多筆資料
```Javascript
db.collection.deleteMany(
  {
    example: /text/
  } 
)
```

### 刪除全部資料
```Javascript
db.collection.deleteMany({})
```

## 練習
參考以下 `selects` collection
```Javascript
{
  "studentName": "Riley Parker",
  "group": "A",
  "score": 83,
  "isPaid": false
},
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
```

1. 指定其中一個 _id ，並將該筆 document 的 group 改為 D
```Javascript
db.students.updateOne(
   {
    _id: ObjectId("2335043b6c3cd13a3a73f0b1f")
   },
   {
    $set: {
      group: "D"
    }
   }
)
```
2. 將 group 為 B 的多筆 document 的 isPaid 改為 true
```Javascript
db.students.updateOne(
   {
    group: "B"
   },
   {
    $set: {
      isPaid: true
    }
   }
)
```
3. 將 studentName 包含關鍵字 Brennan 的 document 刪除
```Javascript
db.students.deleteOne(
   {
    studentName: /Brennan/
   }
)    
```
4. 將 isPaid 為 true 的多筆 document 刪除
```Javascript
db.students.deleteMany(
   {
    isPaid: true
   }
)   
```


以上見解，如有錯誤地方還請留言告知，感謝。