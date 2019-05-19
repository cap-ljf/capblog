# Docker学习总结

## Docker简介
Docker是一个能够把开发的应用程序自动部署到容器的开源引擎。由Docker公司（www.docker.com, 前dotCloud公司，PaaS市场中的老牌提供商）的团队编写，基于Apache  2.0开源授权协议发行。

该引擎的目标就是提供一个轻量、快速的环境，能够运行开发者的程序，并方便高效地将程序从开发者的笔记本部署到测试环境，然后再部署到生产环境。

Docker的目标之一就是缩短代码从开发、测试到部署、上线运行的周期。让你的应用程序具备可移植性，易于构建，并易于协作。

**Docker组件**
- Docker客户端和服务端，也成为Docker引擎；
- Docke镜像；
- Registry；
- Docker容器
- 
### Docker CS架构
Docker是一个C/S架构的程序。Docker客户端只需向Docker服务器或守护进程发出请求，服务器或守护进程将完成所有工作并返回结构。Docke守护进程也称为Docker引擎。Docker提供了一个命令行工具docker以及一整套RESTful API来与守护进程交互。

### Docker镜像
镜像是构建Docker世界的基石。用户基于镜像来运行自己的容器。镜像是基于联合文件系统的一种层式的结构，由一系列指令一步一步构建出来。

### Registry
Docker用Registry来保存用户构建的镜像。Registry分为共有和私有两种。Docker公司运营的公共Registry叫做Docker Hub。也可以架设自己的私有Registry。

### 容器
Docker可以帮用户构建和部署容器，用户只需要把自己的应用程序或服务打包放进容器里即可。我们可以认为，镜像是Docker生命周期中的构建或打包阶段，而容器则是启动或执行阶段。


## 能用Docker做什么
so，了解了容器的这些基本概念，我们能用容器来干什么呢？
- 加速本地开发和构建流程，使其更加高效、更加轻量化。本地开发人员可以构建、运行并发现Docker容器。容器可以在开发环境中构建，然后轻松地提交到测试环境中，并最终进入生产环境。
- 用Docker创建隔离的环境来进行测试；

## Docker入门
关于Docker如何安装，可以搜索“Docker安装 菜鸟教程”。

### Docker命令大全
#### 容器声明周期管理
- run 创建一个新的容器并运行一个命令
- start/stop/restart 启动一个或多个已经被停止的容器、停止一个运行中的容器、重启容器
- kill 杀掉一个运行中的容器。
- rm 删除一个或多少容器
- pause/unpause 暂停容器中所有的进程。恢复容器中所有的进程。
- create 创建一个新的容器但不启动它
- exec 在运行的容器中执行命令
#### 容器操作
- ps 列出容器
- inspect 获取容器/镜像的元数据。
- top 查看容器中运行的进程信息，支持 ps 命令参数。
- attach 连接到正在运行中的容器。
- events 从服务器获取实时事件
- logs 获取容器的日志
- wait 阻塞运行直到容器停止，然后打印出它的退出代码。
- export 将文件系统作为一个tar归档文件导出到STDOUT。
- port 列出指定的容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口。

#### 容器rootfs命令
- commit 从容器创建一个新的镜像。
- cp 用于容器与主机之间的数据拷贝。
- diff 检查容器里文件结构的更改。
#### 镜像仓库
- login 登陆到一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub
- logout 登出一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub
- pull 从镜像仓库中拉取或者更新指定镜像
- push 将本地的镜像上传到镜像仓库,要先登陆到镜像仓库
- search 从Docker Hub查找镜像
#### 本地镜像管理
- images 列出本地镜像。
- rmi 删除本地一个或多少镜像。
- tag 标记本地镜像，将其归入某一仓库。
- build 命令用于使用 Dockerfile 创建镜像。
- history 查看指定镜像的创建历史。
- save 将指定镜像保存成 tar 归档文件。
- load 导入使用 docker save 命令导出的镜像。
- import 从归档文件中创建镜像。
#### info|version
- info 显示 Docker 系统信息，包括镜像和容器数。。
- version 显示 Docker 版本信息。

## Docker镜像
Docker镜像是由文件系统叠加而成。
最低端是一个引导文件系统，即bootfs。当一个容器启动后，它会被移到内存中，而引导文件系统则会被卸载，以留出更多的内存给initrd磁盘镜像使用。
第二层是root文件系统rootfs，它位于引导文件系统之上。
在传统的Linux引导过程中，root文件系统会最先以只读的方式加载，当引导结束并完成了完整性检查之后，它才会被切换为读写模式。但是在Docker里，root文件系统永远只能是只读状态，并且Docker利用联合加载技术又会在root文件系统层上加载更多的只读文件系统。

## Docker构建本地服务
## Docker编配
