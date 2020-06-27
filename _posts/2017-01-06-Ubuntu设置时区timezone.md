---
layout: post
title: Ubuntu 设置时区 timezone
date: '2017-01-06 11:16:28 +0800'
categories:
- 系统运维
tags:
- Ubuntu
comments: []
---
租了一台美国vps，由于时区问题，时间总是和本地相差几个小时

为了方便需要将服务器时间修改为北京时间。我的环境是Ubuntu 16

# 修改配置文件

```
# 将内容修改为 Asia/Shanghai
vi /etc/timezone
```

# 建立软链
```shell
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```
