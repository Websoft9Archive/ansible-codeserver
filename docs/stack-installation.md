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

3. Open the WorkSpace directory at **code-server** console
   ![code-server directory](https://libs.websoft9.com/Websoft9/DocsPicture/en/codeserver/codeserver-openfolder-websoft9.png)

   > Default workspace directory is: */data/wwwroot/codeserver/volumes/config/workspace*  

4. Open the 【Terminal】windows, run the `node` command, you can view the its version
   ![code-server open Terminal](https://libs.websoft9.com/Websoft9/DocsPicture/en/codeserver/codeserver-terminal-websoft9.png)

5. You can install more software by yourself, refer to: [Set Develop Runtime](/solution-runtime.md)

## code-server Setup Wizard

Coming soon...

> More guide about code-server, please refer to [code-server Documentation](https://hub.docker.com/r/linuxserver/code-server).

## Q&A

#### Can't visit the start page of code-server?

Your TCP:80 of Security Group Rules is not allowed, so there is no response from Chrome or Firefox.

#### How can this code-server deploy?

Deploy by Docker, every developer can set different runtime 

#### Insufficient file permissions for files created by code-server?

You can run below command to solve file permission issue

```
chown -R docker.docker /data/wwwroot/codeserver/volumes/config/workspace
```