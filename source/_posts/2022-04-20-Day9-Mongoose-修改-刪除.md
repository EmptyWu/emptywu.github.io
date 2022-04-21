---
layout: post
title: Day9-Mongoose 修改 / 刪除
tags: [Mongoose,Schema,MongoDB,JavaScript]
author: EmptyWu
date: 2022-04-20 22:12:44
category: 資料庫
description: 接續之前，須先建立 Schema、Model 後，再透過 Model 執行修改、刪除 document 等動作
---

## 前言
接續之前，須先建立 Schema、Model 後，再透過 Model 執行修改、刪除 document 等動作

針對 Model 修改、刪除有多個方式（可參考文件），在此列出其中幾個方式
<!--more-->
## Mongoose 修改
### findByIdAndUpdate
修改單筆 ID document
```javascript
const Room = mongoose.model('Room', roomSchema);
// 修改特定 Id 的 document
Room.findByIdAndUpdate("621e45063ff3c8af575a7498", {
    "name": "海景雙人房"
}) // id, update
```

### updateOne()
修改單筆特定條件
```javascript
const Room = mongoose.model('Room', roomSchema);
// 修改特定條件的第一筆 document
Room.updateOne(
  {
    "name": "海景雙人房"
  }, {
    "price": 4500
}) 
```

## Mongoose 刪除
### findByIdAndDelete()
```javascript
// 刪除特定 ID 的 documents
Room.findByIdAndDelete("621e45063ff3c8af575a7498") // id
```

### deleteMany()
```javascript
// 刪除所有 rooms collection 中的 documents
Room.deleteMany({})

// 刪除符合特定條件的多個 documents
Room.deleteMany({rating: {$lt: 3}})
```


## 練習

延續之前任務，嘗試修改、刪除手搖飲 documents
1. 尋找一筆 document 並將 ice 改為 去冰，sugar 改為 半糖
```javascript
const Drink = mongoose.model('Drink', drinkSchema);
Drink.updateOne({
    product: '鍚蘭紅茶',
}, {
    ice: '去冰',
    sugar: '半糖',
});
```
2. 以 ID 尋找一筆 document 並將其刪除
```javascript
Drink.findByIdAndDelete('62512e4d3b7985edf504197f');

```
3. 刪除全部 documents
```javascript
Drink.deleteMany({});

```




以上見解，如有錯誤地方還請留言告知，感謝。