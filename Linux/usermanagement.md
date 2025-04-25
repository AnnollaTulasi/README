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
