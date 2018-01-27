# Dreamfly Dependencies

![build](https://travis-ci.org/dreamfly-io/dreamfly-dependencies.svg?branch=master)

为了达到统一依赖版本的目标，遵循spring-dependencies的做法,我们定义了dreamfly-dependencies pom。

`dreamfly.io`下的所有Java项目，在管理第三方依赖的版本时，都将通过我们定义的`dreamfly-dependencies`来进行版本管理。以求做到在多个项目中，对于同一个第三方依赖，尽可能的使用相同版本，最大限度减少版本冲突发生的可能性。

详细使用方式和设计细节，请见:

- [Dreamfly Dependencies文档](https://docs.dreamfly.io/dreamfly-dependencies/)




