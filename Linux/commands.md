**List commands**
```
ls //listing
ls -l //long listing in alphabetical order
ls -lt //latest on top
ls -lr //long listing in reverse order
ls -lrt //old on top
ls -lrth //h is humanredable
ls -la //a is for all along with hiddenfiles
```
[d]  -->directory
[-] --> file
[l] --> link files
linux is case sensitive siva.txt is different from Siva.txt,where as it is different in windows

**File commands**
```
touch <filename> //to create empty file
cat > <filename> // add the content and then click cntl+D,here if we use the cmd again and enter the data it gets overriden
cat <filename> //prints the data
cat >> <filename> //will appendd the data to the existing one
cp <sourcefile> <destination> //copy
rm <filename> //to remove file
```

**Directory**
```
mkdir <name> //creates directory
rmdir <name> //removes only empty dir
rm -r <dirnmar> //recursively removes files in dir
rm -rf <name> //when some file is in open we cannot remove it f is for force
```

**Download**
```
wget <url> //downloads the file
curl <url> //shows on the screen but will not be downloaded
curl <url> -o <path of file oe fname> //will be downloaded to entered filename
```
**Piping** -out put of one commands goes as input to other
```
grep <word-to-search> <file>
cat file | grep word
echo url | cut -d "/" -f3
cut -d "" -f1 //cut command passically custs based on delimiter and f1 f2 are parts after cutting
```

**AWK command**
```
echo url | awk -F "/" '{print $NF}'
awk -F ":" '{print $3F}' <filename>
```

**Head,Tail**
```
head -n 3 <filename>
tail -n 5 <filename>

#If you want 4 to 10 lines in the file
head -n 10 <filename> | tail -n 7 
```

**Find**
```
find <which-location> -name "<file-name>"
find / -name "passwd" //searches in all folders as we gave root ,should have root access to execute this
find / -type d -name "ec2-user"  //searches for folder
find / -type f -name "filename" //searches for file
```

**Debugging**
- DB is running properly but if you are not able to connect to backend then you should check security groups
- sometimes ping is disabled in servers,can checck for telnet
```
ping ip //whether it is connecting to ip or not
telnet ip port 
curl http://localhost/health //here local host is current server
netstat -lntp
ps -ef | grep <name>
```