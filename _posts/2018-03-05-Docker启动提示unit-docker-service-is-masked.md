---
layout: post
title: 'Docker启动提示Unit docker.service is masked.'
date: '2018-03-05 15:22:38 +0800'
categories:
- 系统运维
tags:
- Docker
comments: []
---
# 环境

- Ubutntu

# 启动

```shell
systemctl start docker
```

# 提示

> Failed to start docker.service: Unit docker.service is masked.

# 解决方案

执行如下三条指令

```shell
systemctl unmask docker.service
systemctl unmask docker.socket
systemctl start docker.service
```
