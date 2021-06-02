# More

Each of the following solutions has been proved to be effective and we hope it can give you help.

## Binding Domain

The precondition for binding a domain is that code-server can accessed by domain name.

When there is only one website on the server, you can visit the website without binding domain. While considering the server security and subsequent maintenance, **Binding Domain** is necessary.

Steps for binding code-server domain are as follows:

1. Connect your Cloud Server;
2. Modify [Nginx vhost configuration file](/stack-components.md#nginx),and change the **server_name**'s value to your domain name.
   ```text
   server
   {
   listen 80;
   server_name www.example.com;  # change it into your domain name
   ...
   }
   ```

## Reset Password

You can't reset code-server by web console, you should reset it by recreate container:

1. Use SFTP to login server, and modify **APP_PASSWORD** in the [.env file](/stack-components.md#code-server) code-server directory
   ```
   APP_VERSION=latest
   APP_PORT=9001
   APP_PASSWORD=123456
   ```
2. Recreate code-server container
   ```
   sudo docker-compose up -d
   ```

## Modify port

Modify port is same with reset password, the difference is just modify the **APP_PORT** value

## Multi-developer

The current deployment scheme has only one code-server by default. Since it does not support multiple users, it is not suitable for multiple development scenarios of collaborative work.  

So how can we support the collaborative use of code-server by multiple developers? Designed from a macro perspective, it needs to be used by multiple developers. Each developer can allocate the following resources to achieve this requirement:

1. Allocate a host port separately
2. Assign a code-server directory separately
3. Run a code-server container separately

You can refer the below sample:  

1. Run the below command to create new code-server directory for new user
   ```
   # CP directory to new folder user1
   cd /data/wwwroot
   cp -r codeserver user1

   # Delete the old data
   rm -rf user1/volumes
   ```

2. Edit the */data/wwwroot/user1/.env* file, set the you value for **APP_PORT,APP_PASSWORD,APP_CONTAINER_NAME**, save it
   ```
   APP_PORT=9001
   APP_PASSWORD=123456
   APP_CONTAINER_NAME=codeserver
   ```
   > APP_PORT and APP_CONTAINER_NAME must different from the already existing code-server


3. Recreate code-server for new user
   ```
   cd /data/wwwroot/user1
   sudo docker-compose  up -d
   ```