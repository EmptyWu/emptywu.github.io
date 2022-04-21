---
layout: post
title: Day6-Mongoose的Schema撰寫規則
tags: [Mongoose,Schema,MongoDB,JavaScript]
author: EmptyWu
date: 2022-04-15
category: 資料庫
description: Mongoose 是 MongoDB 的 ODM（Object Data Modeling） 套件，Mongoose 套件會藉由 MongoDB driver 操作資料庫的資料
---

## 前言
Mongoose 是 MongoDB 的 ODM（Object Data Modeling） 套件，Mongoose 套件會藉由 MongoDB driver 操作資料庫的資料。

使用 ODM 可以降低開發和維護成本， ODM 會使用 JavaScript 的物件反映出資料庫中的資料，相對於使用資料庫原生的查詢語言 (SQL)，用 ODM 的方式操作資料庫會更好上手

<!--more-->
### 安裝方式
```javascript
npm install mongoose --save
```

### nodejs 使用 Mongoose 連線 mongoDB 的連線方式
```javascript
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/DataBaseName');
// DataBaseName 為資料庫的名稱，可以改為自己的資料庫名稱
```

### Mongoose Schema 寫法
建立 Schema（資料庫綱要），定義需要哪些資料、型別、是否顯示、預設值…等等。

例:
```javascript
const Schema = new mongoose.Schema({
  title:  String, // String is shorthand for {type: String}
  author: String,
  body:   String,
  comments: [{ body: String, date: Date }],
  date: { type: Date, default: Date.now },
  hidden: Boolean,
  meta: {
    votes: Number,
    favs:  Number
  }
});
```
因此接收到資料，mongoose就依此 Schema 把關資料是否帶入正確。

#### **type**
```javascript
title: {type: String} // 代表 title 需為一個字串
//只有設定型別可以使用簡寫 title: String
```
物件內的型別，可以針對單獨設定
```javascript
title: {
  chinese: {type: String},
  english: {type: String}
} 
```

若 title 為一個陣列，也可指定陣列中資料型別
```javascript
title: [{type: String}] // 若只有設定型別可以使用簡寫 [String]
```

#### **required**
此資料需為必填項目，可以設定 required，並且可客製化錯誤訊息
```javascript
title: {
  type: String,
  required: [true, 'title 為必填']
}
```

#### **default**
若有資料未填寫，也可以設定此資料的預設值
```javascript
title: {
  type: String,
  default: '未命名的文章'
}
```
通常 required 與 default 不會同時使用


#### **select**
資料欄位希望可以被保護，不顯示出來，可以加入 select 設定
```javascript
password: {
  type: String,
  select: false
}
```

#### **enum**
此資料設定型別為 String 或 Number，可以設定 enum 指定需為哪些值
```javascript
author: {
  type: String,
  enum: ['Amy','Bob','Cody']
}
```
### 練習
設計手搖飲的 Schema，依照以下規則：
1. 產品名稱（product）: 需為字串,必填，若未填寫，錯誤訊息為「產品名稱未填寫」
2. 價錢（price）: 需為數字, 必填，若未填寫，錯誤訊息為「價錢未填寫」
3. 冰塊（ice）： 需為字串, 若未填寫預設為 '正常冰'
4. 甜度（sugar）：需為字串，若未填寫預設為 '全糖'
5. 配料（toppings）：為陣列，內容需為字串

```JavaScript
const drinkSchema = new mongoose.Schema({ 
    product: {type: String,required: [true, '產品名稱未填寫']},
    price: {type: Number,required: [true, '價錢未填寫']},
    ice: {type: String,default: '正常冰'},
    sugar: {type: String,default: '全糖'},
    toppings: [{type: String}]
});
```





以上見解，如有錯誤地方還請留言告知，感謝。