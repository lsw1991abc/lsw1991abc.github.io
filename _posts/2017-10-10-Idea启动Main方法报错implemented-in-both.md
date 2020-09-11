---
layout: post
title: 'Idea启动Main方法报错implemented in both'
date: '2017-10-10 22:57:23 +0800'
categories:
- 编程开发
tags:
- Java
comments: []
---
在使用Idea启动main方法时，提示`Class JavaLaunchHelper is implemented in both Library/Java/JavaVirtualMachines/jdk1.8.0_151.jdk/Contents/Home/bin/java`

在stackoverflow上找到了解决方法：[https://stackoverflow.com/questions/43003012/class-javalaunchhelper-is-implemented-in-two-places](https://stackoverflow.com/questions/43003012/class-javalaunchhelper-is-implemented-in-two-places)

# 原因

> It's the [old bug in Java](https://bugs.openjdk.java.net/browse/JDK-8022291) on Mac that [got triggered by the Java Agent](https://github.com/JetBrains/intellij-community/commit/4fde1be3df5f7c145f943a969eb261e32bf72ef6) being used by the IDE when starting the app. This message is harmless and is safe to ignore.

# 解决方法

1. 使用高版本的JDK。这个问题已经在Java 9 和 8 update 152 中修复。
2. 修改Idea配置。在idea.properties中添加`idea.no.launcher=true`
