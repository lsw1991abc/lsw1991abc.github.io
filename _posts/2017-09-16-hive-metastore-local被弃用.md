---
layout: post
title: hive.metastore.local被弃用
date: '2017-09-16 11:37:07 +0800'
categories:
- 编程开发
tags:
- Hive
comments: []
---
hive.metastore.local


- Default Value: `true`
- Added In: Hive 0.8.1
- Removed In: Hive 0.10 with [HIVE-2585](https://issues.apache.org/jira/browse/HIVE-2585)

Controls whether to connect to remote metastore server or open a new metastore server in Hive Client JVM. As of Hive 0.10 this is no longer used. Instead if [hive.metastore.uris](https://cwiki.apache.org/confluence/display/Hive/AdminManual+MetastoreAdmin#AdminManualMetastoreAdmin-BasicConfigurationParameters) is set then mode is assumed otherwise local.
