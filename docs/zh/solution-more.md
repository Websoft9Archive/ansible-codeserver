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

code-server 无法通过控制台直接修改密码，必须通过重置容器的方式修改密码：

1. 修改 code-server 的 [.env 文件](zh/stack-components.md#code-server)中 **APP_PASSWORD** 的值
   ```
   APP_VERSION=latest
   APP_PORT=9001
   APP_PASSWORD=123456
   ```
2. 重置 code-server 容器后生效
   ```
   sudo docker-compose -f /data/wwwroot/codeserver/docker-compose.yml up -d
   ```

> 重置密码会重新创建容器，即用户额外安装的组件会丢失

## 修改端口

方案与重置密码类似，唯一不同的是需要修改的是 **APP_PORT** 变量的值。

## 多开发者

当前部署方案默认只有一个 code-server，由于它并不支持多用户，所以不合适多开发协同工作的场景。  

那么如何才能支持多开发者协作使用 code-server 呢？从宏观上设计，需多开发者使用，每一名开发者分配如下资源即可实现此需求：

1. 单独分配一个宿主机的端口
2. 单独分配一个 code-server 目录
3. 单独运行一个 code-server 容器

下面是一个范例：

1. 运行下面的命令，将现有的 code-server 整个目录复制一份，命名为：/data/wwwroot/user1
   ```
   # 复制
   cd /data/wwwroot
   cp -r codeserver user1

   # 删除持久数据
   rm -rf user1/volumes
   ```

2. 修改 */data/wwwroot/user1/.env* 文件中的 APP_PORT、APP_PASSWORD、APP_CONTAINER_NAME，然后保存
   ```
   APP_PORT=9001
   APP_PASSWORD=123456
   APP_CONTAINER_NAME=codeserver
   ```
   > APP_PORT和APP_CONTAINER_NAME 必须与当前已经存在的 code-server 容器不同名称，否则无法创建


3. 启动新的 code-server 项目
   ```
   cd /data/wwwroot/user1
   sudo docker-compose  up -d
   ```

由于多用户协同开发有诸多个性化需求，无法在以上方案中一一列出，欢迎提出更多需求。