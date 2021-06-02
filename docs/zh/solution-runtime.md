# 配置环境

code-server 容器默认已经运行 Node, Yarn, Git等工具，可以很方便的配合 code-server 进行 Node 相关程序的开发。  

## 安装组件

若默认环境不符合需求，可以直接通过 **code-server 控制台**安装组件，下面以 JAVA 为例进行说明：

1. 登录 code-server 控制台，在【Terminal】窗口中运行 `sudo su` 切换为 root 用户
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-sudosu-websoft9.png)
   > 密码为 code-server 控制台登录密码

2. 更新 apt 仓库
   ```
   apt update
   ```

3. 安装并验证 Java
   ```
   #1 安装JRE
   apt-get install openjdk-8-jre

   #2 验证版本
   java -version
   ```

## 备份环境

由于 code-server 基于容器运行，如果你打算将容器安装后的环境长期的备份下来，需要参考如下方式创建自定义容器镜像：

1. 登录服务器
2. 运行创建命令命令（基于 codeserver 容器创建一个名称为 codeserver-java 的镜像）
   ```
   #1 创建镜像
   sudo docker commit -m "add java" -a "your name" codeserver codeserver-java:latest

   #2 查看镜像
   sudo docker image ls
   ```
