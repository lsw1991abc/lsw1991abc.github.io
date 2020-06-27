---
layout: post
title: Java Buffer中flip()和rewind()的区别
date: '2017-04-12 09:28:50 +0800'
categories:
- 编程开发
tags:
- Java
- Buffer
comments: []
---
Java在很多读写操作中，需要处理缓冲区重置。Buffer中提供了flip()和rewind()。

两者都可以将当前位置设置为0，但不同的是flip()在重置的同时，会把当前位置设置给界限值。从源码中很容易看出两个方法的区别

```java
public final Buffer flip() {
  limit = position;
  position = 0;
  mark = -1;
  return this;
}


public final Buffer rewind() {
  position = 0;
  mark = -1;
  return this;
}
```
