---
layout: post
title: CSharp-NLog.config紀錄
tags: [C#,.Net,NLog]
author: EmptyWu
date: 2022-04-21 16:37:13
category: C#
description: 每次再寫LOG 紀錄的時候，總會忘記參數設定，這邊紀錄一下，我可能也許會用到NLog 參數設定。
---

## 前言
每次再寫LOG 紀錄的時候，總會忘記參數設定，這邊紀錄一下，我可能也許會用到NLog 參數設定。

## 參數

### Eventlog
```
 <target xsi:type="EventLog"
            name="EventLogTarget"
            source="MyApplicationName"
            eventId="${event-properties:EventId:whenEmpty=0}"
            layout="${message}${newline}${exception:format=ToString}" />
```
source => 可以對應專案名稱

### Layout Options
```
${longdate}
${level:uppercase=true}
${logger}
${message:withexception=true}
``` 

<!--more-->



## 參考來源
1. NLog Config :[https://nlog-project.org/config/](https://nlog-project.org/config/)

以上見解，如有錯誤地方還請留言告知，感謝。