---
sidebarDepth: 3
---

# 参数

code-server 预装包包含 code-server 运行所需一序列支撑软件（简称为“组件”），下面列出主要组件名称、安装路径、配置文件地址、端口、版本等重要的信息。

## 路径

### code-server

本部署方案中的 code-server 基于容器安装，实现开发环境与宿主机隔离。

code-server 安装目录： */data/wwwroot/codeserver*  
code-server docker compose 文件： */data/wwwroot/codeserver/docker-compose.yml*  
code-server 工作目录： */data/wwwroot/codeserver/config/workspace*  
code-server 扩展目录： */data/wwwroot/codeserver/config/extensions*  

### Nginx

Nginx 虚拟主机配置文件：*/etc/nginx/conf.d/default.conf*  
Nginx 主配置文件： */etc/nginx/nginx.conf*  
Nginx 日志文件： */var/log/nginx*  
Nginx 伪静态规则目录： */etc/nginx/conf.d/rewrite*

### MySQL

MySQL 安装路径: */usr/local/mysql*  
MySQL 数据文件 */data/mysql*  
MySQL 配置文件: */etc/my.cnf*    
MySQL 可视化管理参考本文档 [MySQL](/zh/admin-mysql.md) 章节。

### phpMyAdmin

phpMyAdmin 是一款可视化 MySQL 管理工具，在本项目中它基于 Docker 安装。

phpMyAdmin directory：*/data/apps/phpmyadmin*  
phpMyAdmin docker compose file：*/data/apps/phpmyadmin/docker-compose.yml*  

### MongoDB

MongoDB 数据目录: */var/lib/mongodb*  
MongoDB 配置文件: */etc/mongod.conf*  
MongoDB 日志文件: */var/log/mongodb*  
MongoDB 可视化管理参考本文档 [MongoDB](/zh/admin-mongodb.md) 章节。

### adminMongo

adminMongo 是一款可视化 MySQL 管理工具，在本项目中它基于 Docker 安装。

adminMongo directory：*/data/apps/adminmongo*  
adminMongo docker compose file：*/data/apps/adminmongo/docker-compose.yml*  

## 端口号

在云服务器中，通过 **[安全组设置](https://support.websoft9.com/docs/faq/zh/tech-instance.html)** 来控制（开启或关闭）端口是否可以被外部访问。 

通过命令`netstat -tunlp` 看查看相关端口，下面列出可能要用到的端口：

| 类型 | 端口号 | 用途 |  必要性 |
| --- | --- | --- | --- |
| TCP | 80 | 通过 HTTP 访问 code-server 控制台 | 必须 |
| TCP | 443 | 通过 HTTPS 访问 code-server 控制台 | 可选 |
| TCP | 9090 | 通过 HTTP 访问 phpMyAdmin | 可选 |
| TCP | 3306 | MySQL 端口 | 可选 |
| TCP | 9091 | 通过 HTTP 访问 adminMongo | 可选 |
| TCP | 27017 | MongoDB 端口 | 可选 |

## 版本号

组件版本号可以通过云市场商品页面查看。但部署到您的服务器之后，组件会自动进行更新导致版本号有一定的变化，故精准的版本号请通过在服务器上运行命令查看：

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
