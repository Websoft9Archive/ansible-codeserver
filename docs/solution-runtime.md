# Setup Develop Runtime

code-server container have installed **Node, Yarn, Git** by default, if you want to more develop runtime you can install them by yourself.

## Install software

You can install more software by **code-server console**, the below is installing Java for you:

1. Login to code-server console, and open the【Terminal】windows, then run the command `sudo su` 
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/codeserver/codeserver-sudosu-websoft9.png)

   > Password is the same with code-server console

2. Update apt repository
   ```
   apt update
   ```

3. Install Java and verify it
   ```
   #1 Install JRE
   apt-get install openjdk-8-jre

   #2 Check Java version
   java -version
   ```

## Runtime Backup

Since code-server runs on containers, if you plan to back up the environment after the container is installed for a long time, you need to create a custom container image as follows:

1. Login your server
2. Run the docker commit command to create image
   ```
   #1 Create image
   sudo docker commit -m "add java" -a "your name" codeserver codeserver-java:latest

   #2 Look over image
   sudo docker image ls
   ```