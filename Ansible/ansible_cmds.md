
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
5.to start a service
```
ansible.builtin.service:
  name: mysqld
  state: started
  enabled: yes
```
6.mysql module
```
- name: connect to mysql server
  community.mysql.mysql_info:
    login_user: root
    login_password: ExpenseApp@1
    login_host: ip/route 53 record
  register: mysql_info

- name: printing the mysql info
  ansible.builtin.debug:
    msg: "mysql info is {{ mysql_info }}"

- name: setup password
  ansible.builtin.command: "mysql_secure_installation --set-root-pass {{ mysql_root_password }}
  when: mysql_info.failed is true
```

7. installing using pip
```
ansible.builtin.pip:
  name: PyMySQL
  excutable: pip3.9
```
8. if you want to proceed without exiting even after getting errors
```
ignore_errors: true
```
9. to create users
```
ansible.builtin.user:
  name: expense
```
10. to create file,folder,links
```
ansible.builtin.file:
  path: /app //where the folder has to be created
  state: directory  //it can be file or link ans well and file is default value
```

11. to download files form url (curl)
```
ansible.builtin.get_url:
  url:
  destination: //where it has to be downloaded
  mode: //optional
```
12. zip is archieve and unzip is unarchieve
```
ansible.builtin.unarchieve:
  source:
  destination:
  remote_src: yes //file is not in ansible controller it is in ansible remote machine(nodes)
```

13. to copy:
```
ansible.builtin.copy:
  source:
  destination:
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

* Ansible will connect to nodes,will fetch all the details of the node and then based on their detail like (ubuntu/RHEL),it will execute the appropriate cmds,dnf or aptget
```
{{ ansible_facts }} //all facts can be gathered from this
```
* We can access the variables displayed in ansible_facts by ansible_{var_name}

**CONDITION**
- when keyword is used
```
ansible.builtin.debug:
  msg: "the number {{my_num}} is greater than 10"
when: my_num > 10
```

**LOOPS**
-loop,item keywords are used
```
ansible.builtin.debug:
  msg: "Hi {{ item }}"
loop:
- Tulasi
- Sumathi
- Laxmi
- Dharma
```

* you can install packages with sudo access only
```
ansible.builtin.package:
  name: "{{item.name}}"
  state: "{{item.state}}"
loop:
- {name: 'mysql' ,state:'present'}
- {name: 'git' ,state:'absent'}
```

**FUNCTIONS/FILTERS**
* In ansible we cannot create functions ,but can ues the existing filters
* If you want to create new modules ,then using python programming those has to be developed

**DEFAULT**
```
ansible.builtin.debug:
  msg: "Hi {{ person | default('Tulasi')}}" //person is not defined ,icks the default value
```

**SPLIT**
```
- name: covert string to list
  vars:
    fruit_names: "mango,apple,grapes"
  ansible.builtin.debug:
    msg: "fruits are: {{ fruit_names | split(',') }}" //split will convert the string to list
```

**DICT2ITEM**

```
- name: convert map to list
  vars: 
    course: 
      name: ansible
      duration: 10hrs
  ansible.builtin.debug:
    msg: "Course info {{ course | dict2items }}
```

**IEMS2DICT**

```
- name: convert map to list
  vars: 
    course: 
    - {'key':'name','value':'ansible'}
    - {'key':'duration','value':'10hrs'}
  ansible.builtin.debug:
    msg: "Course info {{ course | items2dict }}"
```

**LOWER**
```
msg: "Hello {{ name| lower}}
```

**UPPER**
```
msg: "Hello {{ name| upper}}
```
**MIN and MAX**
```
- name: print min and max
  vars:
    numbers: [1,3,20,45]
  ansible.builtin.debug:
    msg: "max nubers is {{numbers | max }},min number is {{numbers| min }}"
```
* pip install netaddr
* ansible.utils.ipaddr - to check whether the ip is valid or not
```
- name: check ipaddress is valid or not
  vars:
    ip: "198.168.1.1."
  ansible.builtin.debug:
    msg: "{{ ip |ansible.utils.ipaddr }}"
```

**What if module is not available?**
- shell or command modules are available
- ansible.builtin.shell and ansible.builtin.command

**Diff b/w shell and command module**
shell-->it is like logging inside the server and executing the command,we can access variables,redirections(>,<,>>),and pipe
command--> this is like running the cmds from outside,you will not get access to variables,redirections and pipes and all
- we run simple and basic commands in command module and it is more secure as we aare not giving access to everything
- for complex commands we use shell module

**in shell we used to run $(linux_cmd) and stored the output in a variable,this can be acheived in ansible via register**
```
- name: execute command
  ansible.builtin.command: ls -lrt
  register: command_result
- name: access the register
  ansible.builtin.debug:
    msg: "{{ command_result }}"
```
* in this stdout is o/p,rc is return code,stderr is error
* In shell we have to check whether the package is installed r not but in ansible it will install if it is not present(IDEMPOTENT nature for ansible)
* instead of keeping the ip address we can even keep the route 53 records in inventory file
** if we create variables beside ip then they are host variables,if we create seperately then they are group variables**

```
nslookup mysql.tulasi.site //ip mapped will be displayed
```
```
[all:vars]
ansible_user="ec2_user"
ansible_password="DevOps321"
```