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