* Create User and add user to any group
* /etc/passwd has all the user details
* /etc/group contains group information
```
sudo su -
useradd <username>
id <username> //will give user details
passwd <username> //sets p/w to the username
groupadd <gnmae> //creates group
usermod -g <gname> <username> //adds user to the group ,g is primaryGroup
usermod -aG <gname> <username> //appends secondary group to the user
userdel <uname> //deletes user but all groups will not be deleted if primary group is not same as user then it will not be deleted
groupdel <gname> //deletes group name
usermod -g <gname> <uname>//usermod -g ramesh ramesh //removes other primary groups and whenwe delete entire group and user will be deleted
```

* Linux follows key based authentication by default,to enable password based authentication we should do some configurations
```
vim /etc/ssh/ssh_config //set password authentication as true
systemctl restart ssh  //to reflect the changes we should do restart
sshd -t //will not have error if configuration is correct
```


**PERMISSIONS**
* in ls -l we get file owner,group and others details
* Owners or root user can change the permissions
user/owner - u
group - p
others - o

read - 4
write - 2
execute - 1

```
chmod o+w <filename> //write access to owner
chmod o-r <filename> //removes read access to others
chmod ugo+rwx <filename>
chown -R <unmae>:<gname> <file>  // just changes the ownership
chmod 700 -R .ssh //only suresh get all access others will not have any access
```

**Package Management**
/etc/yum.repos.d - it has some ,in which from which we should download,those details are present
* usually one package depends on other package
* yum and dnf are same
```
dnf install git -y
dnf remove git -y
dnf update git - y
dnf list installed //already installed
dnf list available //cna be installed
```

**Service Management**
ssh port 22
```
systemctl status sshd //to check whether in the port the application 
dnf install nginx -y
systemctl start nginx
systemctl status nginx
systemctl stop nginx
systemctl restart nginx
systemctl enable nginx // services will start automatically if not enabled we have to start manually
```

**Process management**
* In linux everthing is process
* PPID - Parent process Id
* foreground and backgroud process
* foreground process will block the system Eg: sleep 10

```
ps //running process
ps -ef // all process
sleep 100 & // runs in background
kill processid // to kill the process wich is struck - request to stop 
kill -9 pid //order to kill will definitely kill
```

**Network Management**
```
netstat -lntp //can see whether the service is running or not
systemctl status nginx
ps -ef | grep nginx
```

