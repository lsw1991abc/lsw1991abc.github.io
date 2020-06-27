---
layout: post
title: Gradle打包可执行jar
date: '2017-05-10 11:46:46 +0800'
categories:
- 编程开发
tags:
- Gradle
comments: []
---
为了使用Gradle打包一个可执行jar，使用`java -jar xxx.jar`可以方便的测试jar包是否有效

在`resources/META-INF`下新建文件`MANIFEST.MF`

```
Manifest-Version: 1.0
Main-Class: lol.xbug.test.Application
```

在`build.gradle`中添加

```
jar {
    manifest {
        attributes "Main-Class" : "lol.xbug.test.Application"
    }
    from {
        configurations.compile.collect {
            it.isDirectory() ? it : zipTree(it)
        }
    }
}
```

然后执行Gradle的task jar，就可以产出jar文件
