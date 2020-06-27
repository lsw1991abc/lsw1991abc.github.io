---
layout: post
title: "@EnableDiscoveryClient、@EnableEurekaClient的区别"
date: '2017-11-01 23:24:09 +0800'
categories:
- 编程开发
tags:
- Spring
- Spring Cloud
comments: []
---
在使用Spring Cloud Eureka服务发现的时候提到了两种注解，一种为`@EnableDiscoveryClient`,一种为`@EnableEurekaClient`

可参考地址：[https://stackoverflow.com/questions/31976236/whats-the-difference-between-enableeurekaclient-and-enablediscoveryclient](https://stackoverflow.com/questions/31976236/whats-the-difference-between-enableeurekaclient-and-enablediscoveryclient)

Spring Cloud中的服务发现有许多种实现，例如`Eureka`、`Consul`、`ZooKeeper`等等。`@EnableDiscoveryClient`基于spring-cloud-commons，`@EnableEurekaClient`基于spring-cloud-netflix

- 如果用Eureka作为注册中心，推荐@EnableEurekaClient
- 如果是其他的注册中心，推荐@EnableDiscoveryClient

# EnableEurekaClient

```java 
/**
 * Convenience annotation for clients to enable Eureka discovery configuration
 * (specifically). Use this (optionally) in case you want discovery and know for sure that
 * it is Eureka you want. All it does is turn on discovery and let the autoconfiguration
 * find the eureka classes if they are available (i.e. you need Eureka on the classpath as
 * well).
 *
 * @author Dave Syer
 * @author Spencer Gibb
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
public @interface EnableEurekaClient {

}
```

# EnableDiscoveryClient

```java
/**
 * Annotation to enable a DiscoveryClient implementation.
 * @author Spencer Gibb
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@Import(EnableDiscoveryClientImportSelector.class)
public @interface EnableDiscoveryClient {

	/**
	 * If true, the ServiceRegistry will automatically register the local server.
	 */
	boolean autoRegister() default true;
}
```
