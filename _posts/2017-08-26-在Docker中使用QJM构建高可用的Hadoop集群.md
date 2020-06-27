---
layout: post
title: 在Docker中使用QJM构建高可用的Hadoop集群
date: '2017-08-26 19:18:45 +0800'
categories:
- 编程开发
tags:
- Hadoop
comments: []
---
本想使用现有的轮子学习Hadoop，但是本着自己动手丰衣足食的心态，还是自己造一个轮子吧。

主要的资料来源，最好不过官方文档：[http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HDFSHighAvailabilityWithQJM.html](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HDFSHighAvailabilityWithQJM.html)

整体的结构如图所示。在Hadoop2.x中，为了使多个NameNode共享信息，所以出现了中间绿色部分的JournaleNode。ZK是为了NameNode的调度。其他就不做解释了

![](http://xbug.xyz/wp-content/uploads/2017/08/dockercomposes_hadoop-ha-qjm-1024x616.png)

# 步骤说明

docker-compose.yml请参考GitHub [https://github.com/lsw1991abc/dockercomposes/tree/master/hadoop-ha-qjm](https://github.com/lsw1991abc/dockercomposes/tree/master/hadoop-ha-qjm)

1. 分别进入JournalNode，启动JournalNode

```shell
hadoop-daemon.sh start journalnode
```

2. 进入任意一个NameNode，格式化NameNode数据

```shell
hdfs namenode -format
```

3. 使备NameNode同步主NameNode首先启动主NameNode，也就是第2步操作的NameNode，启动

```shell
hadoop-daemon.sh start namenode
```

4. 然后进入备NameNode，执行同步

```shell
hdfs namenode -bootstrapStandby
```

5. 初始化NameNode信息到ZK。在任意NameNode节点执行。（在实验过程中，遇到NameNode无法连接ZK问题，原因是ZK自己启动出现了问题导致的）

```shell
hdfs zkfc -formatZK
```

到这里，节点的初始化已基本结束

6. 停止所有节点，并重新启动
```shell
stop-dfs.sh

start-dfs.sh 
start-yarn.sh
```

# 完成！！！

文件的说明请参考GitHub。如有问题，欢迎留言，共同学习！
