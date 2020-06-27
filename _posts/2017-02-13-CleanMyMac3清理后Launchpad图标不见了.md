---
layout: post
title: CleanMyMac3清理后Launchpad图标不见了
date: '2017-02-13 22:10:58 +0800'
categories:
- 分享
tags:
- CleanMyMac
comments: []
---
有的人在用CleanMyMac3清理后Launchpad图标丢失，那么该如何恢复这个图标呢？有兴趣的小伙伴一起来看看吧。

在这里推荐一个非常简单的方法，使用终端重置Launchpad ，将Launchpad恢复成出场设置，进终端输入：

```shell
rm ~/Library/Application\ Support/Dock/*.db
killall Dock
```

CleanMyMac3清理后Launchpad图标丢失的问题就OK了！

