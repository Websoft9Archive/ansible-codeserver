# Start or Stop the Services

These commands are required when you use the code-server of Websoft9.

### code-server

```shell
sudo docker start codeserver
sudo docker stop codeserver
sudo docker restart codeserver
sudo docker stats codeserver

# you can run the CMD in the code-server container by this way
sudo docker exec -it codeserver bash
```

### phpMyAdmin

```shell
sudo docker start phpmyadmin
sudo docker stop phpmyadmin
sudo docker restart phpmyadmin
sudo docker stats phpmyadmin
```

### adminMongo

```shell
sudo docker start adminmongo
sudo docker stop adminmongo
sudo docker restart adminmongo
sudo docker stats adminmongo
```

### Docker

```shell
sudo systemctl start docker
sudo systemctl stop docker
sudo systemctl restart docker
sudo systemctl status docker
```

### Nginx

```shell
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl status nginx
```

### MySQL

```shell
sudo systemctl start mysql
sudo systemctl stop mysql
sudo systemctl restart mysql
sudo systemctl status mysql
```

### MongoDB

```shell
sudo systemctl start mongod
sudo systemctl restart mongod
sudo systemctl stop mongodd
sudo systemctl status mongod
```