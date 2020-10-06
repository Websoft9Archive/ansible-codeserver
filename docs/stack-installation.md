# Initial Installation

If you have completed the code-server deployment, follow the steps below to start a quick use.

## Preparation

1. Get the **Internet IP** on your Cloud Platform.
2. Check your **[Inbound of Security Group Rule](https://support.websoft9.com/docs/faq/tech-instance.html)** of Cloud Console to ensure the **TCP:80** is allowed.
3. Make a domain resolution on your Cloud Console if you want to use domain for code-server.

## code-server Installation Wizard

1. Use local Chrome or Firefox to access the URL *http://DNS* or *http://Cloud Server Internet IP*. You will enter login page of code-server.
   ![code-server login websoft9](https://libs.websoft9.com/Websoft9/DocsPicture/en/codeserver/codeserver-login-websoft9.png)

2. Log in code-server web console. ([Don't have password?](/stack-accounts.md#codeserver)) 
   ![code-server console websoft9](https://libs.websoft9.com/Websoft9/DocsPicture/en/codeserver/codeserver-consolegui-websoft9.png)

3. 在 code-server 界面上打开 workspace 文件夹  
   ![code-server 打开项目目录](https://libs.websoft9.com/Websoft9/DocsPicture/en/codeserver/codeserver-openfolder-websoft9.png)
   > 默认存放代码的根目录为：*/data/wwwroot/codeserver/config/workspace*  

4. 打开 Terminal，查看系统环境（默认已安装 Node, Yarn等）
   ![code-server 打开Terminal](https://libs.websoft9.com/Websoft9/DocsPicture/en/codeserver/codeserver-terminal-websoft9.png)

5. 根据需要进入 code-server 容器[配置所需的环境](/solution-runtime.md)

> More guide about code-server, please refer to [code-server Documentation](https://hub.docker.com/r/linuxserver/code-server).

## Q&A

#### Can't visit the start page of code-server?

Your TCP:80 of Security Group Rules is not allowed, so there is no response from Chrome or Firefox.

#### 本部署方案中 code-server 是如何安装的？

本部署方案中的 code-server 基于 Docker 安装，实现开发环境与宿主机隔离。

#### code-server 创建文件出现文件权限不足的问题？

如果上传的文件存在一些文件权限需要修正。运行如下命令即可解决文件权限问题：

```
chown -R docker.docker /data/wwwroot/codeserver/config/workspace
```