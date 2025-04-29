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