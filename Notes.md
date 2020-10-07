#### 如何获取 code-server 密码？
```
docker exec -i codeserver sudo cat /home/coder/.config/code-server/config.yaml
```
上述命令可以获取密码，且不会进入容器的交互式窗口

#### 镜像选取

当前选择的是：https://hub.docker.com/r/linuxserver/code-server   
它比官方提供的镜像更方便自定义配置

#### 无法通过 Nginx 转发后登录访问？
