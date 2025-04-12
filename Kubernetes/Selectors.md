# Taints and Tolerations,Affinity and Anti affinity
**ERRORS**
1.ErrImagePull  ->node is not able to pull the image
2.CrashLoopBackoff  -> container is unable to start
3.Pending ->worker node not available in AZ,PVC is not bound to PV
4.Container Creating --> pb with PV and PVC

**TAINT** :Paint or pollute
- if we tainted a node,scheduler will not schedule any podson to that node
```
kubectl taint node ip hardware=gpu:NoSchedule
kubectl taint node ip-192-168-41-95.ec2.internal hardware=gpu:NoSchedule-  //to untaint at last - is added
```
- NoSchedule -order-so definitely it should listen
- PreferNoSchedule -request-can shedule the pod as it is requesting and not ordering
- No Execute -Even the one currently running will also evicts

**TOLERATIONS**
- allow
- in nodeselector we add the another AZ ,instead of adding the nodes AZ ,then the pod will be in pending state for long time
- even when the node is tainted,when tolerations exists ,then it will allow
- Scheduler will check whether the nodes are tainted,then it checks the tolerations,if tolerations are present then scheduler will allow to create pods

** If tolerations are created on tainted nodes,scheduler will create the pods on the tainted one without tolerations the pods are not scheduled on tainted nodes

- without applying toleration if we want to run a pod in tainted node,it will be in pending status only
- when we apply tolerations without nodeselector then it may or maynot schedule the pod in tained one

**NODE AFFINITY**
- has more options than node selector
- if resources are not available then it shows pending state

*LABLING NODES
```
kubectl label nodes ip-192-168-41-95.ec2.internal hardware=gpu
```
**SITUATION**

node is tainted --> can scheduler run the pod on that node? --> no
node is tainted --> pod asks for toleration --> can scheduler run the pod --> may be(if resources are not free or scheduler decided another node) --> Running
node is tainted --> pod asks for toleration and nodeSelector --> If tainted have resources(Running) --> if tainted nodes don't have any resources(Pending)

requiredDuringSchedulingIgnoredDuringExecution --> Schedule the pod and execute --> hard rules, labels must be availalbe while scheduling
preferredDuringSchedulingIgnoredDuringExecution --> Soft rule --> if labels are not availalbe then consider schedule on the node.

* in nodeselector we can only specify only one key value pair but in node affinity we can have multiple key value pairs
* wights are present in node affinity and which has less weight is preffered first

**POD AFFINITY**
* Where ever the pod-1 is created ,there the pod-2 has to be created in this cases podAffinity is used
* in pod anti-affinity it will not select that paarticular node

# Ingress Controller
* to expose our application to ouside world we can use nodeport or loadBalancer service but they give classical LB
* Application load balancer(ALB) is intelligent -->host based routing
1.setup ingress controller
2.Use ingress resources -->routing rules
R53--> ALB-->Listener-->Rule-->Target Group(VM/pods)

* Installation is in k8s-ingress folder and ingress controller is named as AWS Load Balacer Controller
**INGRESS RESOURCE**
- From LB it reaches Ingress and based on routes it hits different services
- ALB is a external resource and annotations are used to refer external resource
- Target group,routing all can be set using the ingress resource
- here wehave to mention which one has to be to used http or https
- As we are using https for outside world should attach cerificate
- In R53 the domain details(main atleast without records) should present
- AWS Certificate manager (ACM)-->create certificate for your domain *.tulasi.site-->validation and then attach the arn of the certificate in your manifest
- group has to be added in ingress resource
- **in ingress resource we have path based rules as well as host based rules,we should select according to our requirement**
- **Through ingress contoller applications running in kubernetes will have external access**
- **Using Ingress Resource we can create ALB,Listener,Rule,TargeGroup**
- **Ingress is attached to service,so it fetches the pods and adds them to target group**
- For LB we get one DNs but when we hit that we cannot acces the application as we set the rule that we should hit app1
- so need to paste the DNS in R53
- group is added in ingress resource ,so that only rules will be added to it further instead of creating new lb again and again

***
# Role based Access Control
- Authentication and Authorization purpose
- User,Role,Role binding
- role should be bounded to user through role binding
- eks is one platform and aws is another platform we will not create different users for each platform instead we try to use IAM service
- IAM >Polity>create policy for describing cluster,and then create user and attach the policy created
- We have created role and binded it to user but eks doesn't know what users are present in IAM users ,the authentication b/w eks and IAM can be done from aws-auth
- In aws-auth we have to add user and group so that the authentication will be established
```
aws configure --profile <user> //to add the credentilas of that particular user
aws sts get-caller-identity
```
- Role contains the details of what resources can be accessed
- Namespace level access can be given by role and role binding
- Cluster level access can be given by cluster role and cluster role binding
- nodes,pv are cluster level

# Service Account
* it is pod identity with which it can connect with api server and get access to exteral services
* if thw pod wants to get secrets from aws secrett manager  their should be connection b/w eks cluster and aws secret manager
* Service Account is a non-human account 
* for sa(Service account) if it is with in cluster then role and  rolebinding has to be done

1.OIDC
2.Created policy
3.Attach service Account to pod

***
**INIT CONTAINERS**
- they are used to setup the requirement for pod,eb:backed pod can check whether their are proper connections to databease
- they can fetch secrets for pod
- init container runs before the main container runs and can have mutiple init containers,init containers run before to make sure dependent services run fine before our main application
- main container size will be small as init will take up some of the tasks
- we cannot access init containers once after its execution is completed
```
watch kubectl get pods
```
- EFS and EBS are external volumes
- emptyDir(pods temp storage) and hostPath are internal volumes
- all containers inside pod can access emptyDir

# Daemon Set
* Makes sure pod replica runs on every node
* Due to HPA we may get new nodes ,at that time Daemon set makes sure to create the pods in the newly created nodes
* Logs collection,monitority,extra disk adding can be done using Daemon set
* emptyDir - temp storage for pod
* hostPath - filesystem path in the underlying worker node,it is not secure
* pods should not access the hostsfile system directly
* only through daemon set the hostpath should be accessed and that to in readOnly mode so that the files cannot be created ,updated or deleted
* daemon set is the only exception for admins to collect logs using hostPath
