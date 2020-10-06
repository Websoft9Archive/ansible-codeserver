#### 如何获取 code-server 密码？
```
docker exec -i codeserver sudo cat /home/coder/.config/code-server/config.yaml
```
上述命令可以获取密码，且不会进入容器的交互式窗口