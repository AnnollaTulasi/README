
1.to have root access
```
become: yes
```
2.To print any msg
```
ansible.builtin.debug:  
    msg: ""
```
3.to install any package
present-to install
absent: to remove
```
ansible.builtin.package:
    name:
    state:
```
4.to connect to server it self
```
hosts: local
connection: local
```

**VARIABLES**
* they shouls be defined under vars tab and can be used as "{{varname}}"
* If we mention vars in tasks they are applicable only to that task //task level variables
* We can declare all the variables in a file and then call them in plays
```
vars_files:
- <list of filenames can be added>
```
* Getting the var value from prompt
```
vars_prompt:
- name: COURSE //var name
  prompt: Enter course value  
  private: false //the value entered will be visible,by default it is true and it is not visible
```

vars from inventory
* pass them by adding after the servers
```
[local:vars]
COURSE="Devops"
```

- can pass through args
- while executing ansible command and -e (extra arguments) and pass the values
- file is a reserved keyword in ansible
**PREFERENCE**
1.cmd line/args
2.task level
3.files
4.prompt
5.play level (global)
6.inventory
7.Roles