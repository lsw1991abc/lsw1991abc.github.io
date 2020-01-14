---
layout: post
title:  "使用docker启动yapi"
date:   2020-01-14 10:50:00 +0800
categories: ops
tags: docker yapi
---

这个说明是在yapi基础版本上做的打包方式

# 检出代码

首先把代码clone下来

```bash
git clone https://github.com/YMFE/yapi.git vendors
```

# 打包

进入到vendors后,执行打包命令

```bash
ykit pack -m
```

参考 [https://github.com/lsw1991abc/dockerfiles/tree/master/yapi](https://github.com/lsw1991abc/dockerfiles/tree/master/yapi) 的 dockerfile 进行打包镜像

```bash
# 打包
docker build -t lsw1991abc/yapi:custom.1.0

# push到自己的仓库
docker push lsw1991abc/yapi:custom.1.0
```

# 启动

启动时只要把配置文件挂载，映射出端口就可以了

```bash
-v /data/k8s-volume/yapi/config/config.json:/api/config.json -p 3000:3000
```
