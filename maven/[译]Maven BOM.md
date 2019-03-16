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
BOM代表了Bill Of Materials。BOM是一种特殊的POM，