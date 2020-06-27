---
layout: post
status: publish
published: true
title: K8S中CoreDns替换Kube-Dns
author:
  display_name: Wizard
  login: lsw1991abc
  email: lsw1991abc@gmail.com
  url: http://wp.mobe.local
author_login: lsw1991abc
author_email: lsw1991abc@gmail.com
author_url: http://wp.mobe.local
wordpress_id: 1755
wordpress_url: http://xbug.xyz/?p=1755
date: '2018-08-17 17:38:28 +0800'
date_gmt: '2018-08-17 09:38:28 +0800'
categories:
- 系统运维
tags:
- Kubernetes
comments: []
---
在之前的文章里，写了一些使用kubeadm搭建k8s环境的步骤：[kubeadm安装K8S](http://xbug.xyz/1696.html)，使用的版本是1.10.3

最近在新搭一套环境，发现kubelet版本升级到了1.11.2。于是将kube相关的镜像更新到了1.11.2使用的版本：[https://github.com/lsw1991abc/k8s-library/releases/tag/1.11.2](https://github.com/lsw1991abc/k8s-library/releases/tag/1.11.2)

引用：[https://coredns.io/2018/01/29/deploying-kubernetes-with-coredns-using-kubeadm/](https://coredns.io/2018/01/29/deploying-kubernetes-with-coredns-using-kubeadm/)

调整后的初始化脚本

```shell
kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=1.11.2 --node-name=wizard.local --service-dns-domain=wizard.local --service-cidr=10.244.0.0/16 --apiserver-advertise-address=127.0.0.1
```
