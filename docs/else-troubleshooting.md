# Troubleshooting

If you're having trouble with running code-server, here is a quick guide to solve most common problems.

> Most faults about the Instance is closely related to the Instance provider, Cloud Platform. Provided you're sure the fault is caused by Cloud Platform, refer to [Cloud Platform Documentation](https://support.websoft9.com/docs/faq/tech-instance.html).

#### How can I check the error logs?

You can find the keywords **Failed** or **error** from the logs directory: `/data/logs`

#### Can't start code-server service?

Insufficient disk space and memory, incorrect configuration file may cause the failure to start the service. 

It is recommended to first check through the command.

```shell
# Look over the code-server logs
sudo docker log codeserver

# view disk space
df -lh

# view memory rate
free -lh
```

#### Insufficient file permissions for files created by code-server?

You can run below command to solve file permission issue

```
chown -R docker.docker /data/wwwroot/codeserver/volumes/config/workspace
```