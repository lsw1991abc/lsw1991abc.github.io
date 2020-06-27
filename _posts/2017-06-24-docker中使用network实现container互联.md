---
layout: post
title: docker中使用network实现container互联
date: '2017-06-24 17:30:06 +0800'
categories:
- 系统运维
tags:
- Docker
- Network
comments: []
---
在docker network出现之后，不再推荐使用`--link`方式实现多个container的互联。[https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/](https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/)

使用network实现多个container的互联，只需要将container配置到同一个network中便可以实现互联。

```
docker network connect --help

Usage:	docker network connect [OPTIONS] NETWORK CONTAINER

Connect a container to a network

Options:
      --alias stringSlice           Add network-scoped alias for the container
      --help                        Print usage
      --ip string                   IPv4 address (e.g., 172.30.100.104)
      --ip6 string                  IPv6 address (e.g., 2001:db8::33)
      --link list                   Add link to another container
      --link-local-ip stringSlice   Add a link-local address for the container
```

Docker默认创建了3个network，bridge、none、host。这里不做详细介绍。从image创建container的时候，默认会使用bridge，如果想自定义，可以加入参数`--network networkName`

但我在实验过程中，node1和node2都配置在bridge上，但始终ping不通，这是由于docker默认的bridge不支持自动发现服务：[https://docs.docker.com/engine/userguide/networking/#the-default-bridge-network](https://docs.docker.com/engine/userguide/networking/#the-default-bridge-network)

> Containers connected to the default `bridge` network can communicate with each other by IP address. 
> Docker does not support automatic service discovery on the default bridge network. 
> If you want containers to be able to resolve IP addresses by container name, you should use user-defined networks instead. 
> You can link two containers together using the legacy `docker run --link` option, but this is not recommended in most cases.

所以，需要自己创建一个network，然后使用`docker network connect xxx`把需要互通的container连接到同一个network上，就可以相互ping通了.

原本是想找使用`--link`方式实现两个container的相互ping通（`node1 ping node2`和`node2 ping node1`）。发现了这种方式，就很好的解决了这个问题。
