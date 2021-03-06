> 原文地址：[https://www.baeldung.com/spring-maven-bom](https://www.baeldung.com/spring-maven-bom)
> 原文作者：[https://www.baeldung.com](https://www.baeldung.com)
> 本文永久链接：
> 译者：cap_ljf

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

如我们所见，BOM就是一个用dependencyManagement节点管理所有artifact’s 信息和版本的POM文件。

### 2.5 使用BOM文件
在项目中有两种方式使用前面定义的BOM文件，这样就不用担心版本冲突的问题了。

第一种，使用parent节点继承BOM文件。
```xml
<project ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Test</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>Test</name>
    <parent>
        <groupId>baeldung</groupId>
        <artifactId>Baeldung-BOM</artifactId>
        <version>0.0.1-SNAPSHOT</version>
    </parent>
</project>
```
可以看到我们的Test项目继承了Baeldung-BOM。

我们也可以import the BOM。

在大型项目中，继承的方法不是很有效，因为在POM文件里只能继承一个parent。import是另外一种方法来导入BOM文件。

让我们看一下如果在pom文件里import一个BOM文件：
```xml
<project ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Test</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>Test</name>
     
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>baeldung</groupId>
                <artifactId>Baeldung-BOM</artifactId>
                <version>0.0.1-SNAPSHOT</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>
```

### 2.6 覆盖BOM依赖
artifact’s 版本的顺序是：
1. 在我们项目pom里直接声明的artifact’s 版本；
2. 父项目中的版本；
3. import pom里的版本。跟import的顺序有关；
4. 依赖调节

- 我们可以在项目中显示声明artifact的版本
- 如果一个artifact 在两个import的pom里版本不一致，那么以先import的BOM版本为准。

## 3. Spring BOM
我们可能引入一个第三方的库，或者其他Spring 项目，导致引入一个更老的spring版本。如果我们忘记显示的声明依赖关系，会导致意料之外的问题。

为了克服这类问题，Maven提供了BOM依赖的概念。

我们可以 在dependencyManagement节点中导入spring-framework-bom来保证所有Spring的依赖都是相同的version：
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-framework-bom</artifactId>
            <version>4.3.8.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

这样我们就不应在项目中的依赖里声明版本信息，所有版本信息都在BOM文件里。

## 4. 总结
在这篇文章里，我们展示了  Maven Bill-Of-Material 的概念，和如何集中管理POM文件中的artifact’s信息和版本。

简单的说，我们可以继承或者import BOM，来使用它的便利。

本篇文章的示例代码在[github](https://github.com/eugenp/tutorials/tree/master/spring-bom)上

