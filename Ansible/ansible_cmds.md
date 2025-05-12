
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