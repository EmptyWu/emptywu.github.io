---
layout: post
title: windows-VSCode增加到右鍵快捷菜單中
tags: [Windows,VSCode,右鍵菜單]
author: EmptyWu
date: 2022-04-15 09:56:55
category: Windows
description: 有的時候，想要針對資料夾快速的使用VSCode開啟專案，閱讀程式碼，但安裝完卻沒有在右鍵，這時可能就需要一些方法，讓VSCode 出現在右側菜單中。
---

## 前言

有的時候，想要針對資料夾快速的使用VSCode開啟專案，閱讀程式碼，但安裝完卻沒有在右鍵，這時可能就需要一些方法，讓VSCode 出現在右側菜單中。
![](https://i.imgur.com/IFPkvaj.png)

<!--more-->

新增一個檔案，副檔名修改為reg，新增內容如下：
```r
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\*\shell\VSCode]
@="Open with Code"
"Icon"="D:\\Program\\Microsoft VS Code\\Code.exe"
[HKEY_CLASSES_ROOT\*\shell\VSCode\command]
@="\"D:\\Program\\Microsoft VS Code\\Code.exe\" \"%1\""
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\Directory\shell\VSCode]
@="Open with Code"
"Icon"="D:\\Program\\Microsoft VS Code\\Code.exe"
[HKEY_CLASSES_ROOT\Directory\shell\VSCode\command]
@="\"D:\\Program\\Microsoft VS Code\\Code.exe\" \"%V\""
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode]
@="Open with Code"
"Icon"="D:\\Program\\Microsoft VS Code\\Code.exe"
[HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode\command]
@="\"D:\\Program\\Microsoft VS Code\\Code.exe\" \"%V\""
```

雙擊這個文件，之後都選 `是`，這個時候應該就會出現在右鍵選單中。

以上見解，如有錯誤地方還請留言告知，感謝。