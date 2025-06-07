**General errors**:
- build errors
- deployment errors

**Continuous Integration**
- integrate the code continuosly
* code compile,dependencies install,zip them (create artifact),or build the image,push the image to central repo
**SHIFT LEFT** : building,scanning,testing the application in DEV env itself
- whatever code we write and push to git is cloned into a server,dependencies install,scan the code,and will zip and form the artifact
**Process of integrating continuously when developer push the code to remote repository.in cloves clone,compile,install dependencies,do multiple types of scans,run unit tests,create artifact(zip or image)- we follow the shift left process to identify or make sure the code quality at early stage
- We use jenkins for CI
- Jenkins is a plain webserver,jenkins power lies in plugins,if you want jenkins to do some task you need to install plugin or command under jenkins server or node

**Build**
- pre-build,build,post-build
- everthing in jenkins is job

**freestyle vs pipeline**
- cannot restore if something is missed,cannot version control
- pipeline is code,can do version controlso rrestore can be done

**Master /Node or agent architecture**
- all the jobs are delegated to agents by master
- jenkins agent is anoter server
- even in agent java has to be installed
- remoting jar is responsible for connection b/w master and agent
- all different projects cannot be handled by master,so they are delegated to agents

**Declarative vs Scripted**
- Declarative : compilation of pipeline happens at first and then runs
```
pipeline{

}
```
- Scripted: runs one stage after the other and fails
```
node{

}
```
script block is in scripted we involve that in declarative ,so our pipelines are hybrid
