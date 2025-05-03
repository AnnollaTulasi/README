1XX - informational
2XX - Success status code
3XX - redirectional
4XX - Client side error
5XX - server side error

404 -- anything which user is searching is not available
403 -- no enough permissions to access (FORBIDDEN)
401 -- has to login to access (UNAUTHORIZED)
400 -- bad request (has to check the payload which is passed)
405 -- Method Not Found (using wrong methods)
500 -- Internal server error
502 -- bad gateway -- frontend not able to connect to backend due to some security pb
503 -- Service temporarily unavailable --

**LOGS**
/var/log/nginx -- nginx default logs
```
less <filename> //to get running logs ,enter shift+G to move down
tail -f <filename> //running logs -f is follow
```

**Commands to check memory**
```
free -h //to chcek the free space
top // will show which consumes more memory
dnf install htop -y // to install htop
htop //same as top,has some colours
cat /proc/meminfo
```

**List top 10 high memory process**
```
ps aux --sort -%mem | head -n 10
```

**Disk usage**
```
df -hT
du -sh //disk utilization
du -sh /usr/* // in usr dir which consumes more disk
du -sh * // traverse to particular folder and in that which one consumes more disk space can be checked using this cmd
du -sh /*  //gives details of diisk usage of files and folders of root directory
cat /proc/cpuinfo // to get cpu info
```

**LINUX FOLDER STRUCTURE**
* bin contains basic commands like cat,ls etc
* boot conatains booting details
* dev -devices
* etc - extra conf
* home- cantains different usr directories
* lib - contains the libraries of the commands like cat,ls - binaries or dependencies
* mnt - when disk is full temorarily we will move them to mnt
* opt - optional servers-like tomcat or prometheus can be installed here
* proc - contains system info like cpu,mem info,Mem is RAM
* sbin -contains administrative cmds
* var - contains logs --var/lib -- db related logs,var/log,var/lib/docker

