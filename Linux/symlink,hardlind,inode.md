**INODE**
- inode stores the file type,permissions,ownership,file size,timestamp,disk location
```
ls -li //to see the inode information,we will have inode number
stat <filename>
```

**Sym Link/soft link**
- we can create a link to a file
- it is shortcut to actual file
- it points to the original file
- even the symlink points to actual file the inode number is different for link file and actual file
- when we delete actual file ,symlink will break
- we can create symlink for  directories/folders

```
ln -s <filename> <name> //ln -link s-soft
```

**HardLink**
- hardlink will have the inode number same
- it is like copy of the original file
- useful for backup purpose
- when we remove original file the hardlink file will not be deleted
- if all the  files are deleted then the inode will be deleted
- hardlinks cannot be created for directories/folders

```
ln <filenmae> <name> // no need of -s in hardlink
```
**How to find out ,hardlink of a particular file?**
find / -inum <number>