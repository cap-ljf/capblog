# windows同时安装java8和java11

## 安装jdk8
官网（https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html）下载 64bit安装包，大约200多兆。
![1.png](0)
下载完成之后双击运行，默认配置点下一步即可，默认安装位置在 `C:\Program Files\Java`。

然后打开`cmd`输入`java -version`命令：
![2.PNG](1)
出现上图结果说明jdk8安装成功.

## 安装jdk11
现在我们在jdk8的基础上安装jdk11。
首先在官网下载jdk11的安装包
![3.png](2)
双击exe文件，安装完之后，在cmd里输入`java -version`出来的还是java8，接下来设置环境变量，设置完之后就可以根据设置选择生效的jdk版本。

## 设置环境变量
打开windows系统-高级系统设置-高级-环境变量。

在系统变量中设置以下变量：
**JAVA8_HOME**
`C:\Program Files\Java\jdk1.8.0_161`
**JAVA11_HOME**
`C:\Program Files\Java\jdk-11.0.1`
**JAVA_HOME**
`%JAVA11_HOME%`
**CLASSPATH**
``
上面将`JAVA_HOME`设置为`%JAVA11_HOME%`就是选择生效的jdk版本为11，如果想要jdk8生效就改为`JAVA8_HOME`。
