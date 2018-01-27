# 版本升级策略

## 第一公民

在dreamfly dependencies的设计和实现中，有部分依赖非常重要而敏感，我们称为第一公民。这些依赖的版本在升级时要特别小心。

### spring系列

spring系列的版本升级策略：

1. 首先确认spring boot的版本，一般取最新稳定发布版本
2. 以该spring boot依赖的spring版本为spring版本，以保证spring boot/spring的一致性

| dreamfly | spring | spring-boot | spring-cloud |
|--------|--------|--------|--------|
|  0.1.0 |  5.0.2.RELEASE  |  2.0.0.M7 | 2.0.0.M5 |

备注： 目前spring cloud和spring boot的2.0版本都还在milestone阶段，有些乱。

### grpc相关

grpc相关的类库有：

- grpc-java
- grpc依赖的protobuf
- grpc依赖的netty/netty-tcnative-boringssl-static
- grpc依赖的google guava

由于grpc一直处于快速演进中，而dreamfly的策略是紧跟最新版本。因此grpc的版本升级策略是：

1. 选择最新的grpc发布版本
2. 以该grpc版本的依赖版本为准，确认protobuf/netty/guava等的版本

| dreamfly | grpc | protobuf | guava | netty |netty-tcnative-boringssl-static|
|--------|--------|--------|--------|--------|--------|
|  0.1.0 |  1.9.0 | 3.5.1 |  19.0（最新22.0） | 4.1.20.Final（最新4.1.13.Final） | 2.0.7.Final |

目前看除了guava的版本停留在19.0之外，grpc的其他依赖的版本都更新的非常及时。

特别备注: grpc依赖的protobuf的版本是3.5.1，但是protoc的版本是3.5.1-1，不得已只好分别指定：

- protobuf.version：3.5.1
- protoc.version：3.5.1-1

后续版本更新时主要检查这里。

核对版本的方法：

- 在github上找到release的grpc版本对应的tag
- 打开build.gradle文件，所有grpc使用到的依赖都在这个文件中定义
- 典型路径：https://github.com/grpc/grpc-java/blob/v1.5.0/build.gradle

## 标准依赖

以下依赖是定义在standard pom中作为Dreamfly Java项目的标准依赖。

### google guava

参考前面grpc一节，google guava的版本选择以grpc为准。

需要特别留意的是：

- google guava从版本21起要求java8，而grpc目前没有升级java8的计划，因此可能长期停留在版本19，dreamfly也会如此。

### slf4j

slf4j 的版本升级策略是和 sprint-boot 保持一致，以 spring-boot 依赖的 slf4j 版本为准。

| dreamfly | spring-boot | slf4j |
|--------|--------|--------|
|  0.1.0 |  2.0.0.M7  |  1.7.25 |

> 备注: [spring-boot-dependencies的依赖版本查询地址](http://mvnrepository.com/artifact/org.springframework.boot/spring-boot-dependencies)

### logback

logback的版本升级策略是和sprint-boot保持一致，以spring-boot依赖的logback版本为准。

~~尤其注意 spring-boot 依赖的 logback 版本目前比较落后于最新的 logback 版本，但是考虑到目前对最新版本没有特别要求，因此简单跟随 spring-boot 以保持一致。~~

spring boot 2中logback已经升级到最新版本，因此简单跟随spring-boot就好。

| dreamfly | spring-boot | logback |
|--------|--------|--------|
|  0.1.0 |  2.0.0.M7  | 1.2.3 |

### 测试相关

目前用于测试的标准依赖定义和升级策略如下：

- junit： 采用最新版本5.0系列
- assertj： 采用最新版本
- mockito： 采用最新版本
- powermock： 据说目前和junit5有冲突？

| dreamfly | junit | assertj | mockito | powermock |
|--------|--------|--------|--------|--------|
|  0.1.0 |  5.0.3  |  3.9.0 | 2.13.0 | 1.7.3 |

assertj的几个扩展，目前更新都不快，直接使用最新版本：

| dreamfly |  ssertj-guava | assertj-joda-time |
|--------|--------|--------|
|  0.1.0 |  3.1.0  |  2.0.0 |

## 普通依赖

如果没有特别情况，策略就是简单升级到最新。

### redis

| dreamfly |  jedis |
|--------|--------|
|  0.1.0 |  2.9.0  |

### 关系型数据库

| dreamfly |  mysql | postgresql |
|--------|--------|--------|
|  0.1.0 |  n/a  |  n/a  |

### 数据库类库

| dreamfly |  mybatis | mybatis-spring | druid |
|--------|--------|--------|--------|
|  0.2.1 |  n/a  | n/a | n/a |

### 测试相关

测试类的依赖，如无特别情况，通常升级到最新版本。

| dreamfly | h2 | dbunit | cucumber |
|--------|--------|--------|--------|
|  0.1.0 |  1.4.196 | 2.5.4 | 1.2.5 |

## maven plugin

简单使用最新版本即可，另外如果不是发布重大版本，不必升级 maven plugin。




