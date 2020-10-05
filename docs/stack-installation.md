# Initial Installation

If you have completed the code-server deployment, follow the steps below to start a quick use.

## Preparation

1. Get the **Internet IP** on your Cloud Platform.
2. Check your **[Inbound of Security Group Rule](https://support.websoft9.com/docs/faq/tech-instance.html)** of Cloud Console to ensure the **TCP:8161** is allowed.
3. Make a domain resolution on your Cloud Console if you want to use domain for code-server.

## code-server Installation Wizard

1. Use local Chrome or Firefox to access the URL *http://DNS:15672* or *http://Internet IP:15672*. You will enter installation wizard of code-server.
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-login-websoft9.png)

2. Log in code-server web console. ([Don't have password?](/stack-accounts.md#codeserver)) 
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-bk-websoft9.png)

3. Set you new password from: 【Users】>【Admin】>【Permissions】>【Update this user】
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-pw-websoft9.png)

> More guide about code-server, please refer to [code-server Documentation](https://www.codeserver.com/documentation.html).

## Q&A

#### Can't visit the start page of code-server?

Your TCP:15672 of Security Group Rules is not allowed, so there is no response from Chrome or Firefox.

#### code-server service can't start? 