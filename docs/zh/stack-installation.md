# 初始化安装

在云服务器上部署 code-server 预装包之后，请参考下面的步骤快速入门。

## 准备

1. 在云控制台获取您的 **服务器公网IP地址** 
2. 在云控制台安全组中，检查 **Inbound（入）规则** 下的 **TCP:80** 端口是否开启
3. 若想用域名访问 code-server，请先到 **域名控制台** 完成一个域名解析

## code-server 安装向导

1. 使用本地 Chrome 或 Firefox 浏览器访问网址：*http://域名* 或 *http://服务器公网IP*, 进入登录页面
   ![code-server 登录界面](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-login-websoft9.png)

2. 输入密码（[不知道账号密码？](/zh/stack-accounts.md#codeserver)），成功登录到 code-server 后台  
   ![code-server 后台](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-consolegui-websoft9.png)

3. 在 code-server 界面上打开 workspace 文件夹  
   ![code-server 打开项目目录](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-openfolder-websoft9.png)
   > 默认存放代码的根目录为：*/data/wwwroot/codeserver/config/workspace*  

4. 打开 Terminal，查看系统环境（默认已安装 Node, Yarn等）
   ![code-server 打开Terminal](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-terminal-websoft9.png)

5. 根据需要进入 code-server 容器[配置所需的环境](/zh/solution-runtime.md)

> 需要了解更多 code-server 的使用，请参考官方文档：[code-server Documentation](https://hub.docker.com/r/linuxserver/code-server)

## 常见问题

#### 浏览器打开IP地址，无法访问 code-server（白屏没有结果）？

您的服务器对应的安全组 80 端口没有开启（入规则），导致浏览器无法访问到服务器的任何内容

#### 本部署方案中 code-server 是如何安装的？

本部署方案中的 code-server 基于 Docker 安装，实现开发环境与宿主机隔离。

#### code-server 创建文件出现文件权限不足的问题？

如果上传的文件存在一些文件权限需要修正。运行如下命令即可解决文件权限问题：

```
chown -R docker.docker /data/wwwroot/codeserver/config/workspace
```