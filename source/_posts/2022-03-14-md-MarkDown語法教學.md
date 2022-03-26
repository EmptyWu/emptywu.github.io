---
layout: post
title: "MarkDown語法教學"
tags: [md,MarkDown]
date: 2022/03/14
category: MarkDown
description: 為了加快寫文章的速度，小編特別找了網路上寫Blog的一些語法，特別找到了MarkDown這個語言，覺得似乎可以更加方便的攥寫，因此寫了下面此篇的一些小技巧，與大家分享。
author: EmptyWu
---

## 前言

為了加快寫文章的速度，小編特別找了網路上寫Blog的一些語法，特別找到了MarkDown這個語言，覺得似乎可以更加方便的攥寫，因此寫了下面此篇的一些小技巧，與大家分享。

<!--more-->

#### 標題

```markdown
# H1
## H2
### H3
#### H4
##### H5
###### H6
標題寫法有H1~H6
```

### 字形寫法

##### 粗體

```markdown
__文字__ or **文字**
```

##### 斜體

```markdown
*文字*
```

##### 刪除線

```markdown
~~文字~~
```

### 連接設定

```markdown
[連結](網址) ==> <a href="網址">連結</a> 
[連結](網址 "標題") ==> <a href="網址" title="標題">連結</a>
```

不過因為MarkDown寫法沒有另開視窗，所以寫法還是要使用HTML語法

```html
<a href="網址" target="_blank">連結</a>
```

### 圖片

```markdown
![alt 訊息](圖片路徑 "圖片標題")
```

### 表格

```markdown
|欄位1|欄位2|欄位3|
|----|:---:|----:|
|列1|列2|列3|
|列1|列2|列3|

冒號(colons)代表對齊，放在右邊就是靠右，預設靠左，左右都放就是置中
```

### 水平分隔線

```markdown
-------- 短橫線(Hyphens)
******** 半形星號(Asterisks)
_______  下底線(Underscores)

以上都是分隔線寫法
```

上述還有不足地方，希望大家可以留言給我，也讓我知道還可以有什麼寫法。

參考資料：
[Markdown](https://wastemobile.gitbooks.io/gitbook-chinese/content/format/markdown.html)
