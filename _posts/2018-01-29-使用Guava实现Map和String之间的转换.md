---
layout: post
title: 使用Guava实现Map和String之间的转换
date: '2018-01-29 11:04:35 +0800'
categories:
- 编程开发
tags:
- Java
- Guava
comments: []
---
在Java开发中，可能会遇到Map和String转换的情况，尤其是在HTTP请求的情况下

Guava中提供了`Joiner`和`Splitter`，可以方便的实现两者的互转。位于`com.google.common.base`包下

# Map转String

```java
String string = Joiner.on("&").withKeyValueSeparator("=").join(map);
```

# String转Map

```java
Map<String, String> map = Splitter.on("&").withKeyValueSeparator("=").split(string);
```
