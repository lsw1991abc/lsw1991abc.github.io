---
layout: post
title: Mac 安装 Kubernetes
date: '2018-05-06 16:03:34 +0800'
categories:
- 系统运维
tags:
- Docker
- Kubernetes
comments: []
---
Docker已经宣布在Docker for Mac上支持Kubernetes，虽然现在Stable版本中还没有，但在Edge版本用已经可以看到Kubernetes的启用按钮。

![](http://xbug.xyz/wp-content/uploads/2018/05/kubernetes-docker-for-mac.png)

勾选Enable，点击Apply，之后Kubernetes就会自动安装。但一直在安装，并没有任何进度。

原因是Kubernetes在安装过程中，需要拉取部分镜像，镜像在Google的仓库里，地址：gcr.io。在国内需要访问到这个地址，需要爬个梯子。

而且，直接pull的时候也会提示超时信息

> Error response from daemon: Get https://k8s.gcr.io/v2/: net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)

所以，可以借助外力，将所需要的东西加载到本地。

感谢阿里云提供的minikube，速度还可以。参考 [https://yq.aliyun.com/articles/221687?commentId=17521](https://yq.aliyun.com/articles/221687?commentId=17521)

将k8s的镜像仓库切换到了aliyuncs，其他无变化。使用前，需彻底清理掉之前的`minikube`。

这里虽然使用的是Docker for Mac，但cluster启动的时候，还是需要借助其他的vm来启动。本地安装了`virtualbox`，当然也可以使用`hyperkit`等。

```shell
minikube start --vm-driver=xxx
```

从virtualbox中看到，分别启动了一个docker和一个minikube。

Good Luck
