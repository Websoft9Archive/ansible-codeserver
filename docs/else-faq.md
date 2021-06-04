# FAQ

#### code-server is powered by Microsoft?

No, is powered by [CODER](https://coder.com/)

#### Does code-server support multiple accounts?

No, but you can deploy multiple code-server for different user, refer to: [解决方案](/solution-more.md#multi-developer)

#### Can I install extension for code-server?

Yes

#### Can I reset password of code-server by command?

No, you should reset password by re-create code-server container

#### If there is no domain name, can I deploy code-server?

Yes, access code-server by *http://Cloud Server's Internet IP*.

#### What is the password for the database root user?

The password is stored in the server related file `/credentials/password.txt`

#### Is there a web-base GUI database management tool?

* phpMyAdmin for MySQL, access it by: *http://Cloud Server's Internet IP:9090*
* adminMongo for MongoDB, access it by: *http:///Cloud Server's Internet IP:9091*

#### How to disable phpMyAdmin and adminMongo for Internet user?

You should disable the 9090 and 9091 port at security group of Cloud console, and you can stop the services also

```
sudo docker stop phpmyadmin
sudo docker stop adminmongo
```

#### Is it possible to modify the source path of code-server?

Yes, modify it by the [docker-compose file](/stack-components.md#code-server)

#### How to change the permissions of filesystem?

Change owner(group) or permissions as below:

```shell
chown -R docker.docker /data/wwwroot/codeserver
find /data/wwwroot/codeserver -type d -exec chmod 750 {} \;
find /data/wwwroot/codeserver -type f -exec chmod 640 {} \;
```
#### What's the difference between Deployment and Installation?

- Deployment is a process of installing and configuring a series of software to the server in a different order, which is a complex system engineering.  
- Installation is the process of starting the initial wizard after the application is prepared.  
- Installation is simpler than deployment. 

#### What's Cloud Platform?

Cloud platform refers to platform manufacturers that provide cloud computing services, such as: **Azure, AWS, Alibaba Cloud, HUAWEI CLOUD, Tencent Cloud**, etc.

#### What is the difference between Instance, Cloud Server, Virtual Machine, ECS, EC2, CVM, and VM?

No difference. All refer to cloud servers. They are the different terminology used by manufacturers.