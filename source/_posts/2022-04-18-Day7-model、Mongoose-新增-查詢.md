---
layout: post
title: Day7-model、Mongoose 新增 / 查詢
tags: [Mongoose,Schema,MongoDB,JavaScript]
author: EmptyWu
date: 2022-04-18 11:56:41
category: 資料庫
description: 接續前一天，繼續來說明Mongoose的新增 / 查詢部分。
---

## 前言
接續前一天，繼續來說明Mongoose的新增 / 查詢部分。
須先在專案中引入 Mongoose 套件、連線本地端資料庫，並建立 Schema(可參考 Day6 任務)
建立 Model 寫法如下
```javascript
const roomSchema = new mongoose.Schema({ 
    name: String, 
    price: {
        type: Number,
        required: [true, '價格必填']
    },
    rating: Number
});
// 建立 Model
const Room = mongoose.model('Room', roomSchema);
```
mongoose.model() 第一個參數為 Collection 的名稱，第二個參數帶入 Schema

其中需注意第一個參數 Collection 的名稱，Mongoose 會自動視為小寫開頭及改為複數（結尾加 s）
因此 Room Model 實際上是連接至名稱為 rooms 的 Collection

接著可以使用 Model 新增 document

<!--more-->

### Mongoose 新增
寫法如下
```javascript
const Room = mongoose.model('Room', roomSchema);

const testRoom = new Room({
  name: '總統套房單人房',
  price: 2000,
  rating: 4.5
});
testRoom.save()
  .then(() => {console.log('新增資料成功')})
  .catch((error) => {console.log(error)})
```
建立 Model 後，若要使用 Model 新增資料，需先使用 new 建立 Room 的實體（instance），一個 Model 的 instance 就是 document

產生一個 document 後就可以使用 save() 將其儲存到 rooms Collection 中

新增 document 也可以使用另一種方式create()
```javascript
Room.create({
  name: '總統套房單人房',
  price: 2000,
  rating: 4.5
})
```
執行後可以連線至 MongoDB Compass 本地端資料庫 'mongodb://localhost:27017/test'（test 可更換為自己建立的資料庫名稱）查看，若新增成功可以看到 rooms collection 中會有剛剛新增的資料
```javascript
_id: ObjectId('...')
name: '總統套房單人房'
price: 2000
rating: 4.5
__v: 0 
```
### Mongoose 查詢
Model instance 可以使用 .find() 查詢 documents
```javascript
// 查詢所有 documents
Room.find({});

// 帶入篩選條件
Room.find({ name: '總統套房單人房'})
```

### 練習
延續前一天練習的手搖飲 Schema，建立名稱為 Drink 的 Model，並嘗試新增一筆 document

新增 document 內容如下
```javascript
product: '鮮奶茶',
price: 55,
sugar: '微糖'
```

內容
```javascript
const Drink = mongoose.model('Drink', schema 名稱);

const AddSchema = new drinkSchema({
  /* 新增 document 內容 */
    product: '鮮奶茶',
    price: 55,
    sugar: '微糖'
});
AddSchema.save()
  .then(() => {console.log('新增資料成功')});
  .catch((error) => {console.log(error)})
  ;
// 或另一種方式

Drink.create({
  /* 新增 document 內容 */
    product: '鮮奶茶',
    price: 55,
    sugar: '微糖'
});

```

以上見解，如有錯誤地方還請留言告知，感謝。