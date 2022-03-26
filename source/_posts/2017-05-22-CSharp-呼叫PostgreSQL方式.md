---
layout: post
title: "[C#].Net最簡單PostgreSQL連線方式"
tags: [C#,.Net,PostgreSQL]
date: 2017/05/05
category: C#
description: 最簡單PostgreSQL連線方式
author: EmptyWu
---

.NET連接資料庫大部分都使用MSSQL，當你有需要連線到PostgreSQL做存取的時候，對於某些人可能就被考倒了，但其實是很簡單!
<!--more-->
## 關於Npgsql

官方原文意思
> Npgsql is an open source ADO.NET Data Provider for PostgreSQL, it allows programs written in C#, Visual Basic, F# to > access the PostgreSQL database server. It is implemented in 100% C# code, is free and is open source.

照上面的意思，大約是
> Npgsql 是一個open source 的ADO.NET 數據連結方式，它允許在C#、VB、F#語言上連結資料庫。
> 它可以100%在C#執行，且是免費開源。

## .NET連接PostgreSQL教學

.NET連接**_PostgreSQL_**會用到Npgsql.dll這個參考，可以選擇自行下載再加入參考或是由Visual Studio 上面的
<font color="#ff0000;">**NuGet**</font>
搜尋Npgsql，系統則會幫你加入參考，NuGet真是一個方便的東西。

### 到哪下載

> 官方網站：[http://www.npgsql.org/](http://www.npgsql.org/)

## 實際操作步驟

以照下列步驟實作，就可以達成
**SETP.1.新增一個空的專案**

![新增專案](http://i.imgur.com/XSBjuIf.jpg)

**SETP.2.把Npgsql加入參考，當然你也可以選擇使用NuGet來加入**
![加入參考](http://i.imgur.com/S5CGK1P.jpg )
![NuGet](http://i.imgur.com/g1mgZtr.jpg )
![NuGet](http://i.imgur.com/Pb0RdOh.jpg )
![成功加入參考](http://i.imgur.com/5fxXgTK.jpg )
**SETP.3.在程式碼中加入Using**
![程式碼加入參考](http://i.imgur.com/gavdscS.jpg )
**SETP.4.個人的習慣是把讀寫資料庫寫成可以呼叫的函式，方便使用，才部會全部都寫成一堆，不好閱讀**
![加入呼叫DB的方式](http://i.imgur.com/vg2K4ul.jpg )
![加入呼叫DB的方式](http://i.imgur.com/XpyhjlD.jpg )
**SETP.5.最後實際呼叫上面寫好的函式，來執行讀取、新增功能。**
![實際運用呼叫](http://i.imgur.com/ruNf7BA.jpg )
![實際運用呼叫](http://i.imgur.com/8em79kY.jpg )
**SETP.6.實際執行的結果**
![最後執行結果](http://i.imgur.com/XQbpnow.jpg )

## 程式碼放在GitHub供大家參考

[https://github.com/EmptyWu/NET.git](https://github.com/EmptyWu/NET.git)

最後附上影片供參考

<iframe src="https://www.youtube.com/embed/Wbctmph82Xs" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>
