---
layout: post
title: Hexo-相關指令
tags: [Hexo]
author: EmptyWu
date: 2022-01-01
category: Hexo
description: Hexo 常用相關指令紀錄
---

## 快速開始指令

Hexo 常用相關指令紀錄

<!--more-->

### **new** 建立一個新的md

``` bash
$ hexo new [layout] <title>
```
建立一篇新的文章。如果沒有設定 `layout` 的話，則會使用 ``_config.yml`` 中的 `default_layout` 設定代替。如果標題包含空格的話，請使用引號括起來。

### **server** 啟動伺服器 npm 可以跑本機測試

``` bash
$ hexo server
```
|選項|描述|
|-----|----|
|`-p`, `--port` |覆蓋連接埠設定|
|`-s`, `--static` | 只使用靜態檔案|
|`-l`, `--log` | 啟動記錄器，或覆蓋記錄格式|

### **generate** 產生靜態的html網頁

``` bash
$ hexo generate
```
|選項|描述|
|-----|----|
|`-d`, `--deploy` |產生完成及部屬網站|
|`-w`, `--watch` | 監看檔案變更|


### **deploy** 部屬至github上面

``` bash
$ hexo deploy
```
|選項|描述|
|-----|----|
|`-g`, `--generate` |部署網站前先產生靜態檔案|

### **clean** 清除快取

``` bash
$ hexo clean
```
清除快取檔案 (`db.json`) 和已產生的靜態檔案 (`public`)。

### **list** 列出網站資料

``` bash
$ hexo list <`type`>
```
type 格式: page, post, route, tag, category


參考: [hexo]](https://hexo.io/zh-tw/docs/commands.html)
