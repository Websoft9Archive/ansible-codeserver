#### 如何获取 code-server 密码？
```
docker exec -i codeserver sudo cat /home/coder/.config/code-server/config.yaml
```
上述命令可以获取密码，且不会进入容器的交互式窗口

#### 镜像选取

当前选择的是：https://hub.docker.com/r/linuxserver/code-server   
它比官方提供的镜像更方便自定义配置

#### 无法通过 Nginx 转发后登录访问？

这个取决于 Nginx 的配置，参考：https://github.com/cdr/code-server/blob/master/doc/guide.md#nginx

```
server {
    listen 80;
    listen [::]:80;
    server_name mydomain.com;

    location / {
      proxy_pass http://localhost:8080/;
      proxy_set_header Host $host;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection upgrade;
      proxy_set_header Accept-Encoding gzip;
    }
}
```

重点是
```
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection upgrade;
proxy_set_header Accept-Encoding gzip;
```

使用docker版codeserver时，安装某些环境（例如安装jdk1.8）无源，怎么解决？
```
sudo apt update
sudo apt install openjdk-8-jdk 
```

这三行其什么作用，还需进一步研究 Nginx
