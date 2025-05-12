```
DAYS=${1:-14} // if user is not providing it will take 14 as default else which ever is provided in args will be considered
if [ -d $SOURCE_DIR ] //to check whether the folder is present or not -d is dir -f is file
if [ -n "$Files" ] //to check whether the var is non-empty or empty//-z can also be used
find dir -name filename -mtime +14 | zip -@ folder //all the files will be zipped
```

**CRON TAB**
- Schedules the scripts at particular time
- Should give full path in the crobtab to execute the script
```
crontab -e //for editing //add the time and the script to be executed in crontab,just opens like vim
crontab -l //for listing
var/log/cron //logs will be stored in this
$0 will take the entire file name absolute path
```

**How to make our scripts like commands**
- copy them to /usr/local/bin/filename

**DISADVANTAGES OF SHELL**
**Not Idempotent**
**Error Handling**
**Not Scalable**-when we have too many servers
**Homogeneous** --we write code for redhat and it will not work for ubuntu,some cmds differ Eg: dnf ,apt get

echo $PATH -will give some paths,the commands are stored in these paths
- we should copy the file in too /usr/local/bin/file for customized commands and should give execute access
- when we move the file into different locations it is difficult for the cache to load the changes,we should run hash -r to reload
```
hash -r
```
/usr/local/bin --customized commands
/usr/bin --system cmds for normal user
/usr/local/sbin --customized super user commands
/usr/sbin --System super commands

**Why the command added in customized commands doesn't work in crontab?**
crontab env is minimal,it only searches the commands in /usr/bin,we have to mention the path seperately
```
PATH= /usr/bin:bin:/usr/local/bin
****** backup SOURCE_DIR DEST_DIR
```

* Dev is for devices,xfs is for files a,similar to harddisk and should be monitored
* With % we cannot compare the numbers ,so cut it and then compare
* \n or <br> is used to have the content in newline but it should be enabled in echo state to reflect
echo -e ""

**How do you run other scripts from current shell script?**
we can 2 shell files,and can call the other file by sh filename in the file,variables cannot be y both have different proceess
*to use the variables of other file source ./filename
```
sh <filenmae>  it runs in different process and can't access variables in different file
source <fullpath> process is same here,so we can access the variables
```