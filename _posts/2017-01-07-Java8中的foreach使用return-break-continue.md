---
layout: post
title: Java8中的foreach()使用return/break/continue
date: '2017-01-07 10:28:39 +0800'
categories:
- 编程开发
tags:
- Java
comments: []
---
在使用lambda表达式处理集合时，发现不能使用`break`和`continue`

如果要实现在普通for循环中的效果时，可以使用`return`来替代。

[http://stackoverflow.com/questions/23996454/terminate-or-break-java-8-stream-loop](http://stackoverflow.com/questions/23996454/terminate-or-break-java-8-stream-loop)

意思是说在lambda中使用return时，只是返回当前的遍历，并不会终止下一次循环。所以说，`return`的作用相当于`continue`

而想实现break的效果，可以粗暴点使用`Exception`
