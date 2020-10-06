# 配置环境

code-server 容器默认已经运行 Node，可以很方便的配合 code-server 进行 Node 相关程序的开发。  

如果默认环境不符合您的需求，可以通过如下三个步骤配置您所需的环境：

1. 在服务器上运行如下的命令，进入 coder-server 容器
   ```
   sudo docker exec -it codeserver bash 
   ```
2. 在容器中运行安装命令，配置所需的运行环境（以安装 JRE 为例）
   ```
   #1 apt更新
   sudo apt update

   #2 安装JRE
   apt-get install openjdk-8-jre

   #3 测试java
   java -version
   ```
3. Ctrl+D 退出容器，然后再服务器中运行如下命令基于当前容器创建镜像
   ```
   #1 创建镜像
   sudo docker commit -m "add java" -a "your name" codeserver codeserver2:latest

   #2 查看镜像
   sudo docker image ls
   ```
