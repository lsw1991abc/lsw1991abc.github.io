---
layout: post
title: K8S中，Pod一直处于pending状态
date: 2018-05-31 18:16:10 +0800
categories: ops
tags: Kubernetes
---
在之前的分享中，使用kubeadm创建了一个单节点的Kubernetes：[http://xbug.xyz/1696.html](http://xbug.xyz/1696.html)

使用yml创建一个nginx的deployment：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: default
spec:
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.11.13
        ports:
        - containerPort: 80
```

应用后，一直显示失败。查看pod信息，一直显示`pending`状态

```shell
kubectl get pods
```

这是因为在一台机器上创建单节点的原因，需要如下配置

[https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/#master-isolation](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/#master-isolation)

```shell
kubectl taint nodes --all node-role.kubernetes.io/master
```

然后就可以看到pod正常了
