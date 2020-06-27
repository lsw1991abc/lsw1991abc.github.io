---
layout: post
title: Java8中Date转换为LocalDate
date: '2017-01-06 14:37:57 +0800'
categories:
- 编程开发
tags:
- Java
- Date
comments: []
---
在Java 8中使用了新的时间日期 java.time

全新 API 的众多好处之一就是，明确了日期时间概念，例如：瞬时（instant）、期间（duration）、日期、时间、时区和周期。

同时继承了 Joda 库按人类语言和计算机各自解析的时间处理方式。不同于老版本，新 API 基于ISO标准日历系统， java.time 包下的所有类都是不可变类型而且线程安全。

将Date转换为LocalDate的小示例

```java
Date input = new Date();
Instant instant = input.toInstant();
ZonedDateTime zdt = instant.atZone(ZoneId.systemDefault());
LocalDate date = zdt.toLocalDate();
```

更多小示例可以参考：[Java 8中关于日期和时间API的20个使用示例](http://www.tuicool.com/articles/j2yAve3)
