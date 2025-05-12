**PUSH VS PULL**
- Pull : We can to check
* increases the traffic
* unnecesary resource waste
* cost
* agent is required


- Push : It will give the info when received
- Ansible is based on push based architecture
- Now ansible can even use pull based also
- instead of logging the server and doing the requuired actions,ansible lets to run the commands in background (remotely)
- Ansible(main nde) will connect to other nodes via ssh protocol
- The server which is intalled with Ansible is Ansible node
- Agent is not required
- Ansible can connect to any external system (AWS , Azure,GitHub etc)

**INVENTORY**
- list of servers that ansible is managing
1.Is your ansible server is able to connect the ansible node (firewall,configs has to be checked if it is not connected)
* m is module in ansible
```
anisble -i <ipadd>,all -e ansible_user=ec2_user -e ansible_password=DevOps321 -m ping //when we do ping it will give response as pong
ansible -i <ip>, all -e ansible_user=<> -e ansible_password=<> -m dnf -a "name=nginx state=installed" // -a is for arguments
ansible -i <ip>, all -e ansible_user=<> -e ansible_password=<> -m dnf -b -a "name=nginx state=installed" // -b is execute ass root 
```

**ADHOC COMMANDS**
It is the command issued from ansible server targeting node manually,basically on some emergency/adhoc purpose

* Instead of writing adhoc cmds multiple times,if we write all the commands in a single file it is ansible playbook

**PLAYBOOKS**
Playbook is a list of modules ansible server runs against its nodes

**DATA TRANSFER OBJECTS(DTO)**
YAML,XML,JSON

**PLAYBOOK** - List of plays which contains modules that can do a specific task
