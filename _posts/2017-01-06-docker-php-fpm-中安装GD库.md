---
layout: post
title: docker php fpm 中安装GD库
date: '2017-01-06 10:40:18 +0800'
categories:
- 系统运维
tags:
- PHP
---
运行`docker-php-ext-install gd`发现报错

```
If configure fails try --with-webp-dir=<DIR>
If configure fails try --with-jpeg-dir=<DIR>
configure: error: png.h not found.
```

这时候需要安装`libpng`

```shell
apt-get update
apt-cache search libpng
apt-get install libpng12-dev
```
