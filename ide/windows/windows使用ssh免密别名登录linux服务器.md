由于公司要求卸载盗版xshell和教育版xshell的使用，所以不得不改用其他ssh工具，但是除了xshell其他工具都感觉界面太丑了，搜索查阅一番之后决定使用Cmder + ssh命令搭建一个ssh环境。

## 1. 免密登录原理
### 1.1 SSH简介
SSH（Secure Shell）是一种通信加密协议，加密算法包括：RSA、DSA等。
> RSA：非对称加密算法，其安全性基于极其困难的大整数的分解（两个素数的乘积）；
> DSA：也是非对称加密算法，其安全性基于整数有限域离散对数难题；

### 1.2 SSH免密登陆原理
![image.png](0)


## 2. 使用ssh命令免密登录linux服务器
### 2.1 安装ssh
安装Cmder，或者其他工具，只要能在window下使用ssh命令即可。

### 2.2 本机window下生成私钥公钥
使用`ssh-keygen`命令生成私钥公钥：
```
ssh-keygen -t rsa -f 'xxx' -C "xxx"
```
-t参数指定密钥类型，-f指定生成的密钥文件名称 -C提供一个新注释（如果生成github和gitlab的文件要使用邮箱账号）

### 2.3 将公钥拷贝到linux服务器
```
cat xxx.pub
```
将公钥内容拷贝，然后登陆linux服务器，在~/.ssh/auto