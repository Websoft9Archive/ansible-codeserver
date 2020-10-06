# FAQ

#### code-server 是 Microsoft 开发的吗？

不是，它是由一家名为[CODER](https://coder.com/)的公司开发的

#### code-server 支持多账号吗？

不支持，但我们在本部署包中提供了曲线[解决方案](/zh/solution-more.md#多开发者协同)

#### code-server 支持扩展安装吗？

支持

#### 如何退出 code-server 界面？

暂时没有找到退出界面

#### 是否可以通过命令行修改 code-server 后台密码？

不支持

#### 如果没有域名是否可以部署 code-server？

可以，访问`http://服务器公网IP` 即可

#### 数据库 root 用户对应的密码是多少？

密码存放在服务器相关文件中：`/credentials/password.txt`

#### 是否有可视化的数据库管理工具？

内置 phpMyAdmin，访问地址：*http://服务器公网IP:9090*
内置 adminMongo*http://服务器公网IP:9091*

#### 如何禁止外界访问phpMyAdmin 和 adminMongo？

可以关闭安全组 9090 和 9091 端口，也可以通过下面的命令停止服务

```
sudo docker stop phpmyadmin
sudo docker stop adminmongo
```

#### 是否可以修改code-server的源码路径？

可以，通过修改 [docker-compose 文件](/zh/stack-components.md#code-server)实现

#### 如何修改上传的文件权限?

```shell
# 拥有者
chown -R docker.docker /data/wwwroot/codeserver
# 读写执行权限
find /data/wwwroot/codeserver -type d -exec chmod 750 {} \;
find /data/wwwroot/codeserver -type f -exec chmod 640 {} \;
```

#### 部署和安装有什么区别？

部署是将一序列软件按照不同顺序，先后安装并配置到服务器的过程，是一个复杂的系统工程。  
安装是将单一的软件拷贝到服务器之后，启动安装向导完成初始化配置的过程。  
安装相对于部署来说更简单一些。 

#### 云平台是什么意思？

云平台指提供云计算服务的平台厂家，例如：Azure,AWS,阿里云,华为云,腾讯云等

#### 实例，云服务器，虚拟机，ECS，EC2，CVM，VM有什么区别？

没有区别，只是不同厂家所采用的专业术语，实际上都是云服务器
