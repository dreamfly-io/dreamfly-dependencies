# 设计文档

## 实现原理

maven提供了两种依赖管理机制：

1. 通过parent继承

	这种方式，不仅仅可以继承依赖 `<dependencies/>`,还可以继承其他几乎所有元素，包括属性`<properties/>`, 依赖管理 `<dependencyManagement/>` 等。

	parent继承的优点是功能强大，能继承到的内容非常多。优点是继承是无选择的全部都继承，因此容易继承到超过实际需要的东西。另外，parent只能指定一个，因此非常受限。

2. 通过import导入

	这个方式只能导入`<dependencyManagement/>`，不能导入其他，包括最希望导入的`<properties/>`。

    优点是可以import多个，而且import进来的依赖是加入`<dependencyManagement/>`，不会直接变成项目依赖，可以在`<dependencies/>` 中按照项目实际需要再逐个选择。

## 实现方式

### 方案

为了达到统一依赖版本的目标，参考spring-boot-dependencies的做法，我们的方案如下：

1. 准备一个dependencies pom，定义目前dreamfly所有的Java项目的依赖及其版本
2. 在各个Java项目中，引入这个dreamfly dependencies pom，直接使用已定义的版本，不再自己设置

在有了dreamfly-dependencies项目之后，我们的项目在管理依赖时，不再需要在每个项目中考虑众多第三方依赖的版本，只需要检查对应的dreamfly-dependencies rom 的版本是否一致。

> 只要dreamfly-dependencies的版本是一致的，则第三方依赖的版本必然是一致的。

这样就将问题从"管理数以百计的依赖版本"简化为"**管理一个依赖版本**"，从而简化日常开发。





