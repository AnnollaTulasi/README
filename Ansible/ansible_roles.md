**ANSIBLE ROLES**
* standard structure of writing playbooks that contains tasks,variables,dependencies,files,templates,libraries
* for code reuse ansible roles are used
* in templates we give the file which we required to be used in code and add j2 to it
* in templates we can keep the variables,and ansible will replace them in run time
* copy will not work in ansible
ansible.builtin.copy: because it searches for the file in server in some locations and it will fail
* only the vars in templates will be replaced
ansible.builtin.template has to be used to get th info correctly
* handlers-notifies when something changes
* in tasks we should mention notify and that same name has to be mentioned in handlers -will only run at paricular times,will not run everytime -eg: restarting of servers
* similar to vars we have defaults which also contains variables and it has less priority
* common task for every module is deployment
* unarchieve will download and extract in src we can give url instead of file
* We can create a common folder and write the code and can include that code in the main code using the below code
```
- name: include common role
  include_role:
    name: common      //folder that has to be included
    tasks_from: main  //file name where tasks are created
```
```
roles
    mysql
        tasks
            main.yaml
        vars
            main.yaml
    backend
        files
            backend.service
        templates
            backend.service.js
        tasks
            main.yaml
        vars:
            main.yaml
    frontend:
        tasks
            main.yaml
        vars:
            main.yaml
        handlers:
            main.yaml

    
ansible.config
inventory.ini
```

**How to control the execution of tasks?**
- Running only particular tasks instead of running all 
- we can have mutiple tags for a task
```
- name:adding tags
  tag: 
    - test
```
ansible-playbook -i inventory.ini -t test - will run only the tags attached code