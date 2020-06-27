---
layout: post
title: warn util.nativecodeloader unable to load native-hadoop library for your platform
date: '2017-07-01 12:11:03 +0800'
categories:
- 编程开发
tags:
- Hadoop
comments: []
---
解决方法

修改`.bashrc`，调整一下`export`

```
... others enviroment variables...
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_COMMON_LIB_NATIVE_DIR"
```

然后刷新下`.bashrc`文件

```shell
source ~/.bashrc
```
