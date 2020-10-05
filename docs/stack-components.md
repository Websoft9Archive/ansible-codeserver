# Parameters

The code-server deployment package contains a sequence of software (referred to as "components") required for code-server to run. Below list the important information, the component name, installation directory path, configuration file path, port, version, etc.

## Path

### code-server

code-server installation directory:  */data/codeserver*  
code-server logs directory:  */data/logs/codeserver*  

### Nginx

Nginx vhost configuration file: */etc/nginx/conf.d/default.conf*    
Nginx main configuration file: */etc/nginx/nginx.conf*   
Nginx logs file: */var/log/nginx*  
Nginx rewrite rules directory: */etc/nginx/conf.d/rewrite* 

### MySQL

MySQL installation directory: */usr/local/mysql*  
MySQL data directory: */data/mysql*  
MySQL configuration file: */etc/my.cnf*    
MySQL Web Management URL: *http://Internet IP/9panel*, get credential from [Username and Password](/stack-accounts.md)

## Ports

Open or close ports by **[Security Group Setting](https://support.websoft9.com/docs/faq/tech-instance.html)** of your Cloud Server to decide whether the port can be accessed from Internet.  

You can run the cmd `netstat -tunlp` to check all related ports.  

The following are the ports you may use:

| Name | Number | Use |  Necessity |
| --- | --- | --- | --- |
| TCP | 80 | HTTP to access code-server | Required |
| TCP | 443 | HTTPS to access code-server | Optional |
| TCP | 3306 | Remote to access MySQL | Optional |
| TCP | 9003 | Use port to access code-server | Optional |
| TCP | 9002 | code-server Document Server on Docker | Optional |
| TCP | 9090 | phpMyAdmin on Docker | Optional |


## Version

You can see the version on product pages at Marketplace. However, after being deployed to your server, the components will be updated automatically, resulting in a certain change in the version number. Therefore, run the command on the server to view the exact version number. 

```shell
# Check all components version
sudo cat /data/logs/install_version.txt

# Linux Version
lsb_release -a

# Nginx  Version
nginx -V

# Java version
java -v

# Docker Version
docker -v

# erlang  Version
yum info erlang
apt show erlang

# code-server version
codeserverctl status | grep code-server*
```
