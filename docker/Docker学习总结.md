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
现在我们来看一下：
- 运行容器
- 容器命名
- 停止容器
- 重启已经停止的容器
- 创建守护式容器
- 查看日志
- 查看容器内进程
- Docker统计信息
- 停止守护式容器
- 自动重启容器
- 删除容器
### Docker命令大全
#### 容器声明周期管理
- run
- start/stop/restart
- kill
- rm
- pause/unpause
- create
- exec
- 


## Docker镜像
## Docker构建本地服务
## Docker编配
