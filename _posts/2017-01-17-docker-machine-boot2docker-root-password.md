---
layout: post
title: docker-machine boot2docker root password
date: '2017-01-17 17:10:09 +0800'
categories:
- 系统运维
tags:
- Docker
comments: []
---
有时候使用ssh进boot2docker的时候，是docker用户，但需要某些root权限，但又不知道root密码。可以使用这种方式切换到root

首先进入ssh

```shell
docker-machine ssh default
```

这里使用的是default，可以根据自己需要修改。默认会是default

```shell
sudo -i
```

这样就可以切换到root了
