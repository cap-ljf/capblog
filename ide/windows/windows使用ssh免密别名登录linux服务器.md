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
将公钥内容拷贝，然后登陆linux服务器，在~/.ssh下看有没有 authorized_keys文件，如果没有就新建一个。把公钥内容追加到authorized_keys里。
修改authorized_keys文件的权限为600，重启服务（也可以不重启）：
```
chmod 600 authorized_keys
service sshd restart
```
然后在本机使用ssh命令重新登录linux服务器，就不用输入密码了：
```
ssh -p 端口 username@host
```
如果你发现还要输入密码，那有可能是本机使用的私钥不正确，可能你的.ssh目录下有多个私钥，可以使用-i命令指定私钥：
```
ssh -i 私钥目录地址 -p 端口 username@host
```

## ssh别名登录
在本机.ssh目录新建一个config文件：
内容如下：

