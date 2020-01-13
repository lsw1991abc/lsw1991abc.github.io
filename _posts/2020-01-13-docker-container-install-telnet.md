---
layout: post
title:  "Docker Container中安装telnet"
date:   2020-01-13 1:30:13 +0800
categories: ops
tags: docker telnet
---

默认的安装命令是`apk add xxx`, 类似于`apt`或`yum`

```bash
apk add telnet
```

但使用以上方式安装telnet并不生效, Alpine 镜像中的 telnet 在 3.7 版本后被转移至 busybox-extras 包中，需要使用 apk 单独安装。方式如下

```bash
apk add busybox-extras
```
