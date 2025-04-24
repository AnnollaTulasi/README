1.EsC
2.Colon/Command Mode
3.Insert mode

**COMAND MODE**
```
:/word //for searching,and n is for finding next
:?word //searches from bottom
:noh //no highlight
:set nu //sets numbers in the file
:set nonu //no numbers
:28 d //deletes 28 line
:3s/<wordtofind>/<wordtoreplace> //substitutes the word for first occurance in 3rd line
:3s/<wordtofind>/<wordtoreplace>/g //substitutes the word for all occurance in 3rd line
:%s/sbin/SBIN/g //replaces the whole file sbin with SBIN
:%d //deletes entire file content
```

**ESC Mode**
```
u //undo
yy //copy
p //paste
10p //pastes the lines 10times
dd //cut
gg //cursor points top
shift+g //cursor points down 
```

* To select multiple lines and do copy paste ,can select shift+V//visual mode and then by arrows can select the required lines