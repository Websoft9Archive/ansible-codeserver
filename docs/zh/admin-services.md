# 服务启停

使用由Websoft9提供的 code-server 部署方案，可能需要用到的服务如下：

### code-server

```shell
sudo systemctl start codeserver-server
sudo systemctl stop codeserver-server
sudo systemctl restart codeserver-server
sudo systemctl status codeserver-server

# you can use this debug mode if code-server service can't run
codeserver-server console
```

### MySQL

```shell
sudo systemctl start mysql
sudo systemctl stop mysql
sudo systemctl restart mysql
sudo systemctl status mysql
```

### Redis

```shell
systemctl start redis
systemctl stop redis
systemctl restart redis
systemctl status redis
```
