**Tier Architecture**
1.DB
2.Application Programming Interface
3.Frontend

* DB and Application Programming Interface tiers are not displayed to the user
* mysql server can be connected via mysql cliend(command line)
* within same server their is no need to login using password

nodejs --> package.json
java --> pom.xml
.NET --> msbuild
requirements.txt --> python
Makefile --> C

* the mentioned are the build file for each programing language which contains depaendency,project name,version,libraries required,we download these build file and can proceed further
* only dnf installed pakages(some) can be enabled to systemctl
* we installed our application manually,so we should create a service to run th eapplication continuously
```
cd /etc/systemd/system //services has to be created in this 
systemctl daemon-reload //after creating service should reload the services
```

**PROXY**-on behalf off
**Forward Proxy**
Server is not aware that client is using the VPN,but client is aware of using VPN   
eg:VPN - to restrict the traffic and monitor VPN is used,ananymous client,Geo Location hiding
**Reverse Proxy**
Server is aware of the proxy,client is not aware
- backend applications are behind reverse proxy servers for security queing
- cache

```
/etc/nginx //nginx home directory
/usr/share/nginx/html //html directory
/etc/nginx/nginx.conf //nginx configuration
```
**How do we change the default port in nginx?**
- We can change it in nginx.conf and restart the service to change the port