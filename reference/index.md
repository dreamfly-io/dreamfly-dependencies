# 参考文档

## 介绍

### 背景

在Dreamfly中，预计会有数十个大小Java项目，每个Java项目都会有或多或少的第三方依赖，这里就有一个麻烦：

**如何在数量众多的项目中，统一管理第三方依赖的版本？**

考虑到随着时间的推移，这些项目分别演进，第三方依赖的版本也跟着升级版本时，版本管理就更加麻烦。

此时出现版本冲突甚至陷入"**Jar地狱**"的可能性就会逐渐增加，因此希望有个简单的方案解决或者缓和这个问题。

### 对策

- 目标：尽可能减少版本冲突发生的可能性
- 对策：在各个Java项目中，对于同一个依赖，尽可能的**使用相同版本**。

最终我们参考 spring-boot-dependencies 的做法，定义了 dreamfly-dependencies。

详细的设计思路和实现细节可以参考`dreamfly-dependencies`的 [设计文档](../design/)

## 使用指南

### 可用的pom

目前提供了两个maven pom文件：

1. dreamfly-dependencies: 定义依赖和版本
2. dreamfly-dependencies-standard: 在 dreamfly-dependencies 的基础上，将部分依赖如 guava,slf4j,logback,junit,mockito,powermock 作为统一标准使用

### 使用方式

maven项目使用dreamfly dependencies时，推荐的使用方式是：

1. 尽量选择从dependencies pom或者standard pom继承

	如果需要standard的依赖定义就选择standard pom，如果没有就直接使用dependencies pom。

    这个方式使用最为简便，可以通过继承得到所有在dependencies/standard pom中定义的依赖，插件等。

2. 如果不能以parent的方式继承，则可以考虑import

	此时只能import dependencies pom，因为standard pom中定义的依赖是无法通过 import来导入的，对于import方式standard pom没有意义，直接使用dependencies pom即可。

#### 以parent的方式使用standard pom

> 注： dreamfly中Java项目，目前都是采用这个方式

在定义项目的maven的pom.xml 时，指定parent为 `dreamfly-dependencies-standard`:

```xml
<parent>
    <groupId>io.dreamfly.dependencies</groupId>
    <artifactId>dreamfly-dependencies-standard</artifactId>
    <version>*.*.*</version>
</parent>
<groupId>Your Group ID</groupId>
<artifactId>Your ArtifactId ID</artifactId>
```

> 具体版本请访问 [dreamfly dependencies 的 release 页面](https://github.com/dreamfly-io/dreamfly-dependencies/releases)。

建议在项目的顶级parent定义中申明parent为`dreamfly-dependencies-standard` 。

然后在需要使用依赖时，只需要简单指定哪些依赖，而不必注明版本:

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

#### 以parent的方式使用dependencies pom

如果不想使用basiccloud-dependencies-standard中定义的标准依赖，也可以选择从 basiccloud-dependencies中继承。

在定义项目的maven的pom.xml时，指定parent为`dreamfly-dependencies`:

```xml
<parent>
    <groupId>io.dreamfly.dependencies</groupId>
    <artifactId>dreamfly-dependencies</artifactId>
    <version>*.*.*</version>
</parent>
<groupId>Your Group ID</groupId>
<artifactId>Your ArtifactId ID</artifactId>
```

项目中声明依赖的方式同上。

### 以import的方式使用dependencies pom

如果不能采用parent的方式，则可以退而求其次，通过import的方式引入到需要到项目的pom 中：

```xml
<dependencyManagement>
    <dependencies>
    <dependency>
    	<groupId>io.dreamfly.dependencies</groupId>
    	<artifactId>dreamfly-dependencies</artifactId>
        <version>*.*.*</version>
        <type>pom</type>
        <scope>import</scope>
    </dependency>
    </dependencies>
</dependencyManagement>
```

注意一定要在**dependencyManagement**中申明 import，不能在dependencies中。

这样dreamfly dependencies pom中定义的依赖就被导入到当前项目的 dependencyManagement中，后面在dependencies中申明需要使用的依赖就可以：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
    </dependency>
</dependencies>
```

但是，需要特别指出的是，在 maven 中，import方式只能导入依赖定义，即 `<dependencyManagement/>`中定义的内容，其他内容都不能继承，限制极大。因此不到万不得已，不建议使用import方式。

