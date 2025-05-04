**Colours enabling in Shell**
\e[31m-- Red
\e[32m--Green
\e[33m --Yellow
\e[0m -- White
```
echo -e "\e[31m HelloWorld \e[0m" //at the end if we don't have white teh colour will be printed to th enext line too
```

**Logging**
- What ever we execute those has to be loggeed
< -- less than is input
> -- greater than is output
1 -- sucesss
2 -- failure
- No concatination using +,can use any other character and combine them
```
ls -l 1>output.log //contains successlogs
lsdjeed -l 2>output.log //contains only when the command fails
ls -l &>output.log //both success and failure logs are stored and the file is overridden
ls -l >output.log //redirecting the output
ls -l &>>output.log //here the file will not be overridden,the o/p willl be appended
```

**LOOPS**
for i in {0..100}
do
    echo $i
done