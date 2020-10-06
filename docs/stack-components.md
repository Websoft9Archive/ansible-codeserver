# Parameters

The code-server deployment package contains a sequence of software (referred to as "components") required for code-server to run. Below list the important information, the component name, installation directory path, configuration file path, port, version, etc.

## Path

### code-server

本部署方案中的 code-server 基于容器安装，实现开发环境与宿主机隔离。

code-server 安装目录： */data/wwwroot/codeserver*  
code-server 日志目录： */data/wwwroot/codeserver/config/data/logs*  
code-server docker-compose 文件： */data/wwwroot/codeserver/docker-compose.yml*  
code-server 工作目录： */data/wwwroot/codeserver/config/workspace*  
code-server Extension 目录： */data/wwwroot/codeserver/config/extensions*  

### Nginx

Nginx vhost configuration file: */etc/nginx/conf.d/default.conf*    
Nginx main configuration file: */etc/nginx/nginx.conf*   
Nginx logs file: */var/log/nginx*  
Nginx rewrite rules directory: */etc/nginx/conf.d/rewrite* 

### MySQL

MySQL installation directory: */usr/local/mysql*  
MySQL data directory: */data/mysql*  
MySQL configuration file: */etc/my.cnf*    
MySQL 可视化管理参考本文档 [MySQL](/admin-mysql.md) 章节。

### phpMyAdmin

phpMyAdmin 是一款可视化 MySQL 管理工具，在本项目中它基于 Docker 安装。

phpMyAdmin directory：*/data/apps/phpmyadmin*  
phpMyAdmin docker-compose file：*/data/apps/phpmyadmin/docker-compose.yml*  

### MongoDB

MongoDB 数据目录: */var/lib/mongodb*  
MongoDB 配置文件: */etc/mongod.conf*  
MongoDB 日志文件: */var/log/mongodb*  
MongoDB 可视化管理参考本文档 [MongoDB](/admin-mongodb.md) 章节。

#### adminMongo

adminMongo 是一款可视化 MySQL 管理工具，在本项目中它基于 Docker 安装。

adminMongo directory： */data/apps/adminmongo*  
adminMongo docker-compose file：*/data/apps/adminmongo/docker-compose.yml*  

## Ports

Open or close ports by **[Security Group Setting](https://support.websoft9.com/docs/faq/tech-instance.html)** of your Cloud Server to decide whether the port can be accessed from Internet.  

You can run the cmd `netstat -tunlp` to check all related ports.  

The following are the ports you may use:

| Name | Number | Use |  Necessity |
| --- | --- | --- | --- |
| TCP | 80 | HTTP to access code-server | Required |
| TCP | 443 | HTTPS to access code-server | Optional |
| TCP | 3306 | Remote to access MySQL | Optional |
| TCP | 27017 | Remote to access MongoDB | Optional |
| TCP | 9090 | phpMyAdmin on Docker | Optional |
| TCP | 9091 | adminMongo on Docker | Optional |


## Version

You can see the version on product pages at Marketplace. However, after being deployed to your server, the components will be updated automatically, resulting in a certain change in the version number. Therefore, run the command on the server to view the exact version number. 

```shell
# Check all components version
sudo cat /data/logs/install_version.txt

# Linux Version
lsb_release -a

# Nginx  Version
nginx -V

# Docker Version
docker -v

# MySQL  Version
mysql -V

# MongoDB version
mongodb -V

# code-server version
docker inspect -f '{{ index .Config.Labels "build_version" }}' codeserver
```
