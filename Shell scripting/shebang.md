**What is Shebang**
- all basic cmds are in bin
- #!/bin/bash - it is the interpreter will verify cmds and syntax
- all the cmds which we entered in sh file should be verified by some system and that can be done by shebang

**how to execute shell scripts**
* sh filename or bash filename
* ./filename to run this you should have execute permissions
* chmod +x filenmae //to get execute access
* ./filename // . is currect folder and file to be executed
* sh filename arg1 arg2
* when we use run time variables editing of fiel will reduce

**Shell commands**
```
read = will wait and takes input
read -s = the entered value is not available
```

**How do we run a command inside shell script**
datevar=$(date)
- the date cmd will run and the value is stored in datevar
- if we give string and add then it will consider strings as 0 ,will not concatinate as different programming languages 
- addition of 50+50=100 ,**devops+prac=0 not devopsprac**

**List**
```
MOVIES=("movie1" "movie2" "movie3")
MOVIES[0]
MOVIES[@] //to get all the list
```

**Special Variables**
```
$@ //all
$# // number of variables
$0 //scriptname
$PWD // current dir
$HOME //home dir of current user
$USER //which user is running the script
$$  //processid of the current script
$! process id of last command in background
sleep 60 & // to run the command in background
$? //to check the exit status
```

**CONDITIONS**
if [ expression ]
then 
    statements
else 
    statements
fi
* -gt,-lt,-eq,-ge,-le //greater than,lessthan,equal,greaterthanequal to,lessthan equal to

**SHELLSCRIPTING**
* Shell will not exit if we have errors,it will proceed to execute,it is our duty to stop it when error occurs
* exit 1,we can put any value other than zero
* for every cmd we should check the exit status
```
id -u //if it returns 0 then it is root user
```