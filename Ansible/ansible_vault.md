**VAULT**
- we will encrpyt the password and store and later after decriptying we utilize it
- all the below requires password to access them,while creating vault file the passwords are also created
- the o/p vault file can be used by vars_file
- ansible only tries to load the data (encrypted data) should use --ask-vault-pass to enter the password and to decrypt
- can mention --ask-vault-pass in ansible.config file too
- we should not interrupt the running program so instead can use --vault-password-file which actually contains the password and this cannot be stored in git,it has to be in server and --vault-password-file path has to be mentioned
- whatever can be added n commandline can be added in ansible.config file

```
ansible-vault create <name.yaml>
ansible-vault view <name>
ansible-vault edit <name>
cat <name.yaml> //this o/p has to be kept in git
```

**Instead of using vault and storing the passwords,we can use ssm_parameter**
```
login_password in mysql=lookup('amazon.aws.aws_ssm',<name>,decrypt=True) //to get password from ssm
```

**Ansible Dynamic Inventory**
- inventory -list of hosts and group of hosts /servers
- we have a plugin in wwhich we mention the details for dynamic inventory
- the name of the file should be like demo.aws_ec2.yaml
- in host all has to be mentioned
```
plugin: amazon.aws.aws_ec2
regions:
  - us-east-1
filters:
  tag:Name: nginx
  instance-state-name: running
hostnames:
  - private-ip-address
compose:
  ansible_host: private_ip_address   //this is for connecting to servers
```

- ansible-playbook -i demo.aws_ec2.yaml
**Fork vs Serial**
- serial is will complete all the tasks in the mentioned servers
- fork is present in ansible.config ,by default its vaule is 5,will connect to 5 servers at a time ,can change the value
