> 原文地址：[https://www.baeldung.com/spring-maven-bom](https://www.baeldung.com/spring-maven-bom)
原文作者：[https://www.baeldung.com](https://www.baeldung.com)
本文永久链接：
译者：cap_ljf

Maven Bom
## 1. 概览
在这篇快速教程中，我们将探究 Maven是怎么使用BOM 的。

## 2. 依赖管理概念
为了理解什么是BOM，我们怎么使用它，我们首先需要知道基本概念。

### 2.1 什么是Maven POM？
Maven POM是一个XML文件，里面包含了Maven用来导入依赖关系和构建项目的信息、配置。

### 2.2 什么是Maven BOM？
BOM代表了Bill Of Materials。BOM是一种特殊的POM，用于控制项目依赖的版本控制，并提供了一个中心地方来定义、升级它们的版本。

### 2.3 依赖传递
Maven 可以自动发现我们的依赖dependencies 依赖的其他项目，并自动导入它们。这其中收集的依赖层级没有数量限制。

当2个依赖引用一个相同artifact的不同版本时会出现冲突。哪一个会被Maven引入呢？

**答案是最近原则。这意味着在项目依赖tree中离我们项目最近声明的版本会被引入，这称为 依赖调节。**

我们用下面的例子来解释依赖调节：
```A -> B -> C -> D 1.4  and  A -> E -> D 1.0 ```
这个例子展示了项目A依赖B和E，B和E自身又依赖于D的不同版本。Artifact D 1.0最终会被项目A引用因为它的path更短。

由于引用了Artifact D 1.0，可能会造成B有问题。有两种不同的方法来决定哪一个版本的artifacts应该被引入：
- 我们总是显示的在pmo文件里声明一个具体的版本。例如，为了引入D 1.4，我们可以在pmo文件里显示声明这个版本的依赖关系。
- 我们可以使用 依赖管理 节点来控制artifact版本，这也是我们接下来要介绍的。

### 2.4 依赖管理
简单的说，依赖管理是集中管理依赖信息的机制。

当我们有一个项目集继承了一个公共的parent，那把所有依赖信息放进一个共享的POM文件里，这个POM文件就称之为BOM。

下面是怎么写BOM文件的例子：
```xml
<project ...>
     
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Baeldung-BOM</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>BaelDung-BOM</name>
    <description>parent pom</description>
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>test</groupId>
                <artifactId>a</artifactId>
                <version>1.2</version>
            </dependency>
            <dependency>
                <groupId>test</groupId>
                <artifactId>b</artifactId>
                <version>1.0</version>
                <scope>compile</scope>
            </dependency>
            <dependency>
                <groupId>test</groupId>
                <artifactId>c</artifactId>
                <version>1.0</version>
                <scope>compile</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>
```

