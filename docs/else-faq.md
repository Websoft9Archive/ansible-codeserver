# FAQ

#### code-server 是 Microsoft 开发的吗？

不是，它是由一家名为 [CODER](https://coder.com/) 的公司开发的

#### code-server 支持多账号吗？

不支持，但我们在本部署包中提供了曲线[解决方案](/zh/solution-more.md#多开发者协同)

#### code-server 支持扩展安装吗？

支持

#### 如何退出 code-server 界面？

暂时没有找到退出界面

#### Can I reset password of code-server by command?

No

#### If there is no domain name, can I deploy code-server?

Yes, access code-server by *http://Cloud Server Internet IP*.

#### What is the password for the database root user?

The password is stored in the server related file `/credentials/password.txt`

#### Is there a web-base GUI database management tool?

内置 phpMyAdmin，访问地址：*http://服务器公网IP:9090*
内置 adminMongo*http://服务器公网IP:9091*

#### 如何禁止外界访问phpMyAdmin 和 adminMongo？

可以关闭安全组 9090 和 9091 端口，也可以通过下面的命令停止服务

```
sudo docker stop phpmyadmin
sudo docker stop adminmongo
```

#### Is it possible to modify the source path of code-server?

可以，通过修改 [docker-compose 文件](/zh/stack-components.md#code-server)实现

#### How to change the permissions of filesystem?

Change owner(group) or permissions as below:

```shell
chown -R docker.docker /data/wwwroot/codeserver
find /data/wwwroot/codeserver -type d -exec chmod 750 {} \;
find /data/wwwroot/codeserver -type f -exec chmod 640 {} \;
```
#### What's the difference between Deployment and Installation?

- Deployment is a process of installing and configuring a series of software to the server in a different order, which is a complex system engineering.  
- Installation is the process of starting the initial wizard after the application is prepared.  
- Installation is simpler than deployment. 

#### What's Cloud Platform?

Cloud platform refers to platform manufacturers that provide cloud computing services, such as: **Azure, AWS, Alibaba Cloud, HUAWEI CLOUD, Tencent Cloud**, etc.

#### What is the difference between Instance, Cloud Server, Virtual Machine, ECS, EC2, CVM, and VM?

No difference. All refer to cloud servers. They are the different terminology used by manufacturers.