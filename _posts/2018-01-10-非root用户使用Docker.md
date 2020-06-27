---
layout: post
title: 非root用户使用Docker
date: '2018-01-10 22:58:38 +0800'
categories:
- 系统运维
tags:
- Docker
comments: []
---
一般来说，我们都是使用root账户权限来运行docker的相关命令，例如docker、docker-compose等

> The docker daemon binds to a Unix socket instead of a TCP port. By default that Unix socket is owned by the user root and other users can access it with sudo. For this reason, docker daemon always runs as the root user.
> 
> To avoid having to use sudo when you use the docker command, create a Unix group called docker and add users to it. When the docker daemon starts, it makes the ownership of the Unix socket read/writable by the docker group.

首选需要创建一个docker组

```shell
sudo groupadd docker
```

然后将当前用户加入docker组内

```shell
sudo gpasswd -a ${USER} docker
```

重新启动docker服务

```shell
sudo systemctl restart docker
```

此时需要退出当前用户重新登陆

运行docker命令可不需要再加sudo

```shell
docker info
```
