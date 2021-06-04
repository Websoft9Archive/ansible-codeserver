# code-server Cloud Installer

![](https://libs.websoft9.com/common/websott9-cloud-installer.png) 

## Introduction

[English](/README.md) | [简体中文](/README-zh.md)  

**code-server Cloud Installer**, developed by [Websoft9](https://www.websoft9.com), is an automatic installation program of [code-server](https://github.com/cdr/code-server) based on Ansible and shell. It helps user install code-server and pre-configure required items automatically and users only need to run a command on Linux. It simplifies the complicated installation and initialization process.  

## System Requirement

System Requirement to install this repository are as following：

| Conditions       | Details                               | Notes                |
| ------------------- | --------------------------------| -------------------- |
| Operating System   | CentOS7.x, Ubuntu18.04, Amazon Linux2 | Optional                 |
| Public Cloud     | AWS, Azure, Alibaba Cloud, HUAWEI ClOUD, Tencent Cloud    | Optional                 |
| Private Cloud     | KVM, VMware, VirtualBox, OpenStack    | Optional                 |
| Server Configuration | vCPU no less than 1 core, Memory no less than  1 GIB, Storage no less than 10 GB, Bandwidth no less than 100M ||

To learn more information, please view [Installation & Configuration](https://github.com/cdr/code-server).

## Ecosystem

Core components of this repository: Apache code-server, Nginx, PostgreSQL, Docker, phpPgAdmin on docker

Learn more about [Parameters](/docs/stack-components.md).

## Installation

You can install it by thi Cloud Installer solution all in one. In addition, you can deploy image published on major Cloud Platform by Websoft9.

#### All-in-one Installer

Run the automatic installation script with **root** authority to start the installation. If necessary, users need to make interactive choices, and then wait patiently until the installation is successful.

```
$ sudo su -
$ wget -N https://raw.githubusercontent.com/Websoft9/ansible-linux/main/scripts/install.sh; bash install.sh -r codeserver
```

If the network is broken or blocked, SSH will be interrupted and the installation will fail. Please reinstall.

#### Image on Cloud 

Follow our [code-server image](https://apps.websoft9.com/codeserver) for installation on major Cloud Platform.

## Documentation

**[Administrator Guide](https://support.websoft9.com/docs/codeserver)** 

## Changelog

Detailed changes are documented in the [CHANGELOG](/CHANGELOG.md).

## License

[LGPL-3.0](/License.md), Additional Terms: It is not allowed to publish free or paid image based on this repository in any Cloud platform's Marketplace.

Copyright (c) 2016-present, Websoft9

This program provided by Websoft9 contains a series of software with separate copyright notices and license terms. Your use of the source code for the software included is subject to the terms and conditions of its own license.

## FAQ

#### Can I run this repository on Ansible Tower? 

Yes.

#### How to install and view the latest release?

This deployment always install the latest version of code-sever, you can get the code-server version from [code-server repository](https://github.com/cdr/code-server/releases), and modify the Ansible variable **[codeserver_version](/roles/codeserver/defaults/main.yml)** to change the code-server version for this repository if you want to install a specific version. 

#### Is the default password safe?

The solution used the random password solution, every deployment produce unique password which is different from other users
