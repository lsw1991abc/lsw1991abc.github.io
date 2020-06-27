---
layout: post
title: docker compose define both links and networks 问题及解决方法
date: '2017-04-06 00:34:38 +0800'
categories:
- 系统运维
tags:
- Docker
comments: []
---
docker compose define both links and networks 问题及解决方法

>  Link to containers in another service. Either specify both the service name and a link alias (SERVICE:ALIAS), or just the service name.</p>
> ```yaml
> web:
>   links:
>     - db
>     - db:database
>     - redis
> ```
> Containers for the linked service will be reachable at a hostname identical to the alias, or the service name if no alias was specified.
Links also express dependency between services in the same way as depends_on, so they determine the order of service startup.
> Notes:
> If you define both links and networks, services with links between them must share at least one network in common in order to communicate.
This option is ignored when deploying a stack in swarm mode with a (version 3) Compose file.

原文地址：[https://docs.docker.com/compose/compose-file/#links](https://docs.docker.com/compose/compose-file/#links)

# 问题复现：

Compose File Version：3

Docker中启动mysql，php-fpm，nginx。由于手动创建了一个network，所以在顶级`networks`里定义了一个`xbug-network`，并且设置`externale:true`

```shell
docker network create xbug-network
```

此时，三个container都需要配置自己的networks为xbug-network。由于之前的习惯，在php中使用了links，将mysql连接到php中。此时php访问数据库时超时。翻看links和networks的资料，找到了这个提示信息。

> Notes:
> If you define both links and networks, services with links between them must share at least one network in common in order to communicate.

由上文看出，需要提供一个共同的网络链接。我已经使用了同一个networks，可还是不行。

# 解决方法：

既然这样，networks不能去掉，那就去掉links好了。可是那又怎样让php知道mysql的地址。仔细看了看services里的networks，得到了以下几点提示。
[https://docs.docker.com/engine/reference/commandline/network_connect/#use-the-legacy---link-option](https://docs.docker.com/engine/reference/commandline/network_connect/#use-the-legacy---link-option)

```shell
docker network connect --link container1:c1 multi-host-network container2
# 或
docker network connect --alias db --alias mysql multi-host-network container2
```

第一种是像links那样，将mysql别名连接到php上。第二种是把mysql别名，其他随便使用

个人觉得这两种方式修改network比较啰嗦。所以采用了以下方式 [https://docs.docker.com/compose/compose-file/#networks](https://docs.docker.com/compose/compose-file/#networks)

以下是我的compose file里部分内容，这样，在php中使用mysql或db就可以找到mysql地址了：

```yaml
services:
  mysql:
    image: mysql
    container_name: mysql
    networks:
      xbug-network:
        aliases:
          - mysql
          - db

  php:
    image: php:fpm
    container_name: php
    depends_on:
      - mysql
    networks:
      xbug-network:
        aliases:
          - php

  nginx:
    image: nginx
    container_name: nginx
    depends_on:
      - php
    networks:
      - xbug-network

networks:
  xbug-network:
    external: true
```
