# 更多...

下面每一个方案，都经过实践证明行之有效，希望能够对你有帮助

## 域名绑定

绑定域名的前置条件是：已经完成域名解析（登录域名控制台，增加一个A记录指向服务器公网IP）  

完成域名解析后，从服务器安全和后续维护考量，需要完成**域名绑定**：

code-server 域名绑定操作步骤：

1. 确保域名解析已经生效  
2. 使用 SFTP 工具登录云服务器
3. 修改 [Nginx虚拟机主机配置文件](/zh/stack-components.md#nginx)，将其中的 **server_name** 项的值修改为你的域名
   ```text
   server
   {
   listen 80;
   server_name codeserver.yourdomain.com;  # 此处修改为你的域名
   ...
   }
   ```
4. 保存配置文件，重启 [Nginx 服务](/zh/admin-services.md#nginx)

## 重置密码

code-server 没有修改密码的功能，必须通过重置容器（会导致已有容器环境丢失）的方式修改密码：

1. 修改 code-server 的 [docker-compose 文件](zh/stack-components.md#code-server)中 **PASSWORD** 的值
   ```
    services:
      code-server:
        image: linuxserver/code-server
        container_name: codeserver
        environment:
          - PUID=1000
          - PGID=1000
          - PASSWORD=12345
          - SUDO_PASSWORD=12345 #optional
          - PROXY_DOMAIN=code-server.my.domain #optional
   ```
2. 重置 code-server 容器后生效
   ```
   sudo docker-compose -f /data/wwwroot/codeserver/docker-compose.yml up -d
   ```

## 容器网络

本项目中，默认将容器的与宿主机共用同一个网络，所以容器所用的端口就会占用宿主机一个端口，这种情况下容器应用与宿主机的数据库可以采用 localhost 连接。  

可以通过如下步骤将容器的网络独立于宿主机：

1. 修改 code-server 的 [docker-compose 文件](zh/stack-components.md#code-server)中 **network_mode** 的值改为 `bridge`
    ```
    network_mode: host
    ```
2. 重置 code-server 容器后生效
   ```
   sudo docker-compose -f /data/wwwroot/codeserver/docker-compose.yml up -d
   ```

一旦 code-server 容器的网络独立于宿主机，容器的访问和连接方式将发生变化：

1. 容器需绑定到宿主机端口才可以被外界访问
2. 容器中连接宿主机数据库就必须使用内网IP地址：127.17.0.1

## 多开发者协同

当前部署方案默认只有一个 code-server，由于它并不支持多用户，所以不合适多开发协同工作的场景。  

那么如何才能支持多开发者协作使用 code-server 呢？从宏观上设计，需多开发者使用，每一名开发者分配如下资源即可实现此需求：

1. 单独分配一些宿主机的端口
2. 单独分配一个存储目录
3. 单独运行一个 code-server 容器

下面是一个范例：

1. 在宿主机服务器上创建一个目录：/data/wwwroot/user1
2. 考虑 code-server 需要与宿主机匹配 【宿主机端口：容器端口】

   * 9010:8443 # code-server 所需的端口
   * 9011:8080
   * 9012:9090

   > 以上将宿主机9010-9012 三个端口分配给新的 code-server 容器

3. 在 /data/wwwroot/user1 目录下创建 docker-compose.yml 文件，将如下内容拷贝进去，修改后保存
   ```
    services:
    code-server:
      image: linuxserver/code-server
      container_name: codeserver
      environment:
        - PUID=1000
        - PGID=1000
        - PASSWORD=password 
        - SUDO_PASSWORD=password #optional
        - PROXY_DOMAIN=code-server.my.domain #optional
      network_mode: host
      volumes:
        - /data/wwwroot/user1/config:/config
      ports:
        - 9010:8443
        - 9011:8080
        - 9012:9090
      restart: unless-stopped

    networks:
      default:
        external:
          name: apps
   ```

   > PASSWORD 项是登录密码，必须修改，否则密码太简单会有安全隐患

4. 启动新的 code-server 项目，通过： http://服务器公网IP:9010 访问 code-server 界面
   ```
   sudo docker-compose -f /data/wwwroot/user1/docker-compose.yml up -d
   ```

5. 修正文件权限
   ```
   sudo chown -R docker:docker /data/wwwroot/user1
   ```

由于多用户协同开发有诸多个性化需求，无法在以上方案中一一列出。如果您在设置中碰到一些技术困扰，请联系人工支持。