# Parameters

The code-server deployment package contains a sequence of software (referred to as "components") required for code-server to run. Below list the important information, the component name, installation directory path, configuration file path, port, version, etc.

## Path

This solution use Docker to deploy all service, you can run the command `docker ps` to list them.  

### code-server

code-server directory： */data/wwwroot/codeserver*  
code-server logs directory: */data/wwwroot/codeserver/volumes/config/data/logs*  
code-server workspace: */data/wwwroot/codeserver/volumes/config/workspace*  
code-server Extension directory: */data/wwwroot/codeserver/volumes/config/extensions*  
code-server docker-compose file: */data/wwwroot/codeserver/docker-compose.yml*  

> The **.env** file at code-server directory include the port,password settings

### Nginx

Nginx vhost configuration file: */etc/nginx/conf.d/default.conf*    
Nginx main configuration file: */etc/nginx/nginx.conf*   
Nginx logs file: */var/log/nginx*  
Nginx rewrite rules directory: */etc/nginx/conf.d/rewrite* 

### MySQL

MySQL installation directory: */usr/local/mysql*  
MySQL data directory: */data/mysql*  
MySQL configuration file: */etc/my.cnf*  

MySQL Web Management refer to [MySQL Management](/admin-mysql.md)

### phpMyAdmin

phpMyAdmin is a visual MySQL management tool, is installed based on docker.  

phpMyAdmin directory：*/data/apps/phpmyadmin*  
phpMyAdmin docker compose file：*/data/apps/phpmyadmin/docker-compose.yml* 

### MongoDB

MongoDB data directory: */var/lib/mongodb*  
MongoDB Configuration File:  */etc/mongod.conf*  
MongoDB logs File:  */var/log/mongodb*  

### adminMongo

adminMongo is a visual MongoDB management tool, is installed based on docker.  

Docker root directory: */var/lib/docker*  
Docker image directory: */var/lib/docker/image*  

### Docker

Docker root directory: */var/lib/docker*  
Docker image directory: */var/lib/docker/image*   
Docker daemon.json: please create it when you need and save to to the directory */etc/docker*   

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
