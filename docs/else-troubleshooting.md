# Troubleshooting

If you're having trouble with running code-server, here is a quick guide to solve most common problems.

> Most faults about the Instance is closely related to the Instance provider, Cloud Platform. Provided you're sure the fault is caused by Cloud Platform, refer to [Cloud Platform Documentation](https://support.websoft9.com/docs/faq/tech-instance.html).

#### How can I check the error logs?

You can find the keywords **Failed** or **error** from the logs directory: `/data/logs`

#### Can't start code-server service?

Insufficient disk space and memory, incorrect configuration file may cause the failure to start the service. 

It is recommended to first check through the command.

```shell
# restart code-server service
systemctl status codeserver
journalctl -u codeserver

# view disk space
df -lh

# view memory rate
free -lh
```

#### Error in Chrome when modify password?

This error has nothing to do with code-server server. Just upgrade you local Chrome to solve it.

![chrome error of code-server](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-chromeerror-websoft9.png)
