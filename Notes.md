# code-server on CentOS.notes

组件名称：code-server on CentOS
安装文档：https://github.com/cdr/code-server
配置文档：https://github.com/cdr/code-server
支持平台： Debian家族 | RHEL家族 | Windows 

责任人：helin

## 概要

- code-server 是一个可以在远程服务器上运行 VS Code 的工具。

  通过浏览器访问，它可以让你：

  - 在 Chromebook、平板电脑和笔记本电脑上都有一致的开发环境。
  - 利用大型云服务器的优势加速测试、编辑与下载等操作。
  - 节能减耗
    - 所有密集计算都在服务器上运行。
    - 不再需要运行多余的 Chrome 实例。

## 环境要求

- 程序语言：Java
- 应用服务器：Nginx
- 数据库：无
- 依赖组件：apache

## 安装说明

### 1.手动安装

```
mkdir /code-server  
cd  code-server                  #创建安装目录并进入
curl -LO https://github.com/cdr/code-server/releases/download/2.1692-vsc1.39.2/code-server2.1692-vsc1.39.2-linux-x86_64.tar.gz  #选择最新的linux版本，通过curl下载code-server
tar -xzvf code-server2.1692-vsc1.39.2-linux-x86_64.tar.gz  #解压code-server
cd cd code-server2.1692-vsc1.39.2-linux-x86_64      #进入文件夹
sudo cp code-server /usr/local/bin           #代码服务器可执行文件复制到，/usr/local/bin以便您可以通过运行以下命令在系统范围内对其进行访问：
sudo mkdir /var/lib/code-server          #为代码服务器创建一个文件夹，该文件夹将存储用户数据
sudo vi /usr/lib/systemd/system/code-server.service  #将服务配置存储在目录中名为的文件code-server.service中/usr/lib/systemd/system，systemd 在其中存储其服务。使用vi编辑器创建它：
/usr/lib/systemd/system/code-server.service
[Unit]
Description=code-server
After=nginx.service

[Service]
Type=simple
Environment=PASSWORD=your_password
ExecStart=/usr/local/bin/code-server --host 127.0.0.1 --user-data-dir /var/lib/code-server --auth password
Restart=always

[Install]
WantedBy=multi-user.target                  #your_password用您想要的密码替换
sudo systemctl start code-server                #启动代码服务器服务
sudo systemctl status code-serve                  #观察其状态来检查它是否已正确启动
sudo systemctl enable code-server                  #设置为在服务器重启后自动启动
```



### 2.使用docker安装

```
yum install docker            #安装docker
systemctl start docker       
systemctl enable docker
docker run -it -p 127.0.0.1:8080:8080 -v "$PWD:/home/coder/project" -u "$(id -u):$(id -g)" codercom/code-server:latest                #安装code-server

```

在本机浏览器输入 localhost:8080 即可访问控制台

## 配置

安装完成后，需要依次完成如下配置

```
netstat -nl|grep 61616          #查看默认端口
防火墙开启activemq端口8161（管理平台端口）和61616（通讯端口）
```

## 服务

本项目安装后不会自动生成

## 常见问题

#### 有没有管理控制台？

*http:// 公网 IP:8080即可访问控制台

输入日志中生成的密码即可登录

```
docker exec -it code-server /bin/bash
cat ~/.config/code-server/config.yaml
```

#### 本项目需要开启哪些端口？

| item         | port  |
| ------------ | ----- |
| 管理平台端口 | 8161  |
| 通讯端口     | 61616 |
| http         | 15672 |

## 日志

- 2020-04-21完成CentOS安装研究





问题：

```
centos7.5 解决缺少libstdc++.so.6库的原因及解决办法

执行node -v报错如下：

[root@bogon ~]# code-server -v
code-server: error while loading shared libraries: libstdc++.so.6: cannot open shared object file: No such file or directory

先加载所有安装包

yum repolist


查看哪个安装包包含该库：

yum provides libstdc++.so.6

执行结果：

[root@bogon ~]# yum whatprovides libstdc++.so.6
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.njupt.edu.cn
 * extras: mirrors.163.com
 * updates: mirrors.njupt.edu.cn
libstdc++-4.8.5-36.el7.i686 : GNU Standard C++ Library
Repo        : base
Matched from:
Provides    : libstdc++.so.6


可以看到安装包 libstdc++-4.8.5-36.el7.i686


安装libstdc++-4.8.5-36.el7.i686
```



