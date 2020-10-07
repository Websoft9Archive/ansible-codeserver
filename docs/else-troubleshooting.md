# Troubleshooting

If you're having trouble with running code-server, here is a quick guide to solve most common problems.

> Most faults about the Instance is closely related to the Instance provider, Cloud Platform. Provided you're sure the fault is caused by Cloud Platform, refer to [Cloud Platform Documentation](https://support.websoft9.com/docs/faq/tech-instance.html).

#### How can I check the error logs?

You can find the keywords **Failed** or **error** from the logs directory: `/data/logs`

#### Can't start code-server service?

Insufficient disk space and memory, incorrect configuration file may cause the failure to start the service. 

It is recommended to first check through the command.

```shell
# 查看 code-server 容器运行日志
sudo docker log codeserver

# view disk space
df -lh

# view memory rate
free -lh
```

#### code-server 在线创建文件权限不足？

如果上传的文件存在一些文件权限需要修正。运行如下命令即可解决文件权限问题：
```
chown -R docker.docker /data/wwwroot/codeserver/config/workspace
```