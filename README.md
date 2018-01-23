# DreamFly Dependencies

![build](https://travis-ci.org/dreamfly-io/dreamfly-dependencies.svg?branch=master)

## English

### Purpose & Strategy

In order to unify all the versions of 3PP dependencies, we define dreamfly-dependencies pom which follows the practice of spring-dependencies.

For all Java projects in `dreamfly.io`, we will reuse dreamfly-dependencies to manege versions of all third-party dependencies. We will try to use the same version of each third-party dependency accross all the projects, so that we can reduce the risk of version conflict as much as possible.

### Instruction

we currently provide two maven pom files:

1. `dreamfly-dependencies`

	It defines all the dependencies and versions as maven `dependencyManagement`

2. `dreamfly-dependencies-standard`

	It's based on foundation-dependencies ，we consider some dependencies as unified standard dependencies to be used in every project, such as guava, slf4j, logback, junit, mockito, powermock, etc...

To use them, just inherite from `dreamfly-dependencies` or `dreamfly-dependencies-standard` by setting maven's parent pom:

```xml
<parent>
    <groupId>io.dreamfly.dependencies</groupId>
    <artifactId>dreamfly-dependencies</artifactId>
    <version>*.*.*</version>
</parent>
```

or if you want to use standard dependencies(Recommanded!):

```xml
<parent>
    <groupId>io.dreamfly.dependencies</groupId>
    <artifactId>dreamfly-dependencies-standard</artifactId>
    <version>*.*.*</version>
</parent>
```

Later when you define your dependencies, you can just simply declare like following examples without specifing versions:

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
</dependency>
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <scope>test</scope>
</dependency>
```

### Documentation

We have provided more detail in documentation:

1. [Reference](https://reference.dreamfly.io/en/dependencies/): about how to use dreamfly-dependencies
2. [Design Documentation](https://reference.dreamfly.io/en/dependencies/): the design of dreamfly-dependencies，implementation detail, as well as consideration of version selection.

## 中文

### 目的和策略

为了达到统一依赖版本的目标，遵循spring-dependencies的做法,我们定义了dreamfly-dependencies pom。

`dreamfly.io`下的所有Java项目，在管理第三方依赖的版本时，都将通过我们定义的`dreamfly-dependencies`来进行版本管理。以求做到在多个项目中，对于同一个第三方依赖，尽可能的使用相同版本，最大限度减少版本冲突发生的可能性。

### 使用方式

目前提供了两个 maven pom 文件：

1. `dreamfly-dependencies`

	定义依赖和版本为maven `dependencyManagement`。

2. `dreamfly-dependencies-standard`

	在dreamfly-dependencies的基础上，将部分依赖作为标准依赖在每个项目中统一使用，如guava, slf4j, logback, junit, mockito, powermock等。

使用时，通过maven的parent继承方式，从dreamfly-dependencies或者dreamfly-dependencies-standard继承：

```xml
<parent>
    <groupId>io.dreamfly.dependencies</groupId>
    <artifactId>dreamfly-dependencies</artifactId>
    <version>*.*.*</version>
</parent>
```

或者如果你想使用标准依赖(推荐!):

```xml
<parent>
    <groupId>io.dreamfly.dependencies</groupId>
    <artifactId>dreamfly-dependencies-standard</artifactId>
    <version>*.*.*</version>
</parent>
```

之后在定义依赖时，就只要简单如下声明即可，无需再指定版本:

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
</dependency>
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <scope>test</scope>
</dependency>
```

### 文档

我们提供了更加详细的文档：

1. [参考手册](https://reference.dreamfly.io/zh/dependencies/): 介绍如何使用dreamfly-dependencies
2. [设计文档](https://design.dreamfly.io/zh/dependencies/): 介绍dreamfly-dependencies 的设计思路，实现细节，以及对版本选择的考虑

