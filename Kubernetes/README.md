# CONCEPTS

Kubernetes Cluster setup,pods,containers,labels,annotations,Instances,CrashLoopBackoff,EVN,ConfigMap,Secret,Service,
***

**Kubernetes**
- When the containers increases it is difficult to manage them,so for orchestration purpose kubernetes came into picture
- eksctl is used to create ,update and delete clusters
- images are already created and how to interact with images is discuussed in manifest files
- EKS is useful fr creating the control plane(master) and in the nodegroup(nodes) we should attach the ec2 instances
- kubectl is to interact with the cluster
- We cannot simply connect to cluster,authentication is required

**Authentication to cluster**
- aws configure (aws cli)
- IAM Role

**Kuberneters Cluster Setup**
1.create one linux server as workstation
2.install docker to build images
3.Run aws configure to provide authentication
4.eksctl to create cluster
5.kubectl to interact with cluster

**Instances**
- Ondemand : creating server on spot ,costly
- Reserved : booking/reserving the server before as it is planed before
- Spot : when the desired capavity is not used they will provided the resources on discounts--Availablity is not guaranteed--with 2 min notice the hardware will be removed when the aws itself requires
* Spot is not used for PROD only for testing we can use

**CLUSTER CREATION CMD**
```
eksctl create cluster --config-file=eks.yaml
eksctl delete cluster --config-file=eks.yaml
```

- Isolation in kubernetes is achieved by namespace
- Workstation is the common server which is in betwwn our system and kubernetes cluster
- the kubernetes manifest file are cloned into the server and when we use kubectl commands and apply the manifest file it is applied into the cluster

**Difference b/w create and apply**
create throws error if already the manifest is created
- apply will create only when the manifest file is not created else just shows warning instead of throwing error

docker-->image-->container
k8s-->image-->pod

**POD Vs CONTAINER**
* Pod is the smallest deployable component,Pod can have one or many containers

**CRASHLOOPBACKFF**
* When a image is runned ,if it is not started restarts will happen and even after restart if the container is not up then we get CRASHLOOPBACKOFF error

# The container should run infinite time so that it will not exists and only then the application is available to the outside world
* For nginx the code to run infinitely is present as the image is already create by different people
*But for almalinux we should create the cmd to run the conainer infinitely

* If we have 2 containers in the yaml file we can enter different container by the below command
```
kubectl exec -it <pod_name> -c <container_name> -- bash

```

* All containers in the pod share the same ip and storage
* Logs of a pod are available until it is up
* ELK is to store logs,even if the server is deleed,we cannot have logs
* sidecar container access the storage of the server and pushes the logs outside(ELK)

**Labels vs Annotations**
* Labels are for selecting internal resources
* annotations are for selecting external resources and can have special characters like :// (links)

**ENV**
- we can have list of ENV with key and value pairs

**ALIAS**
'''
alias ka="kubectl apply -f"
'''

**REQUESTS vs LIMITS**
- Request are minimum requirements of memory and CPU,and Limits are maximum requirements of memory and CPU

**CONSUMPTION DETAILS**
CPU and memory consumption of the pod can be checked as below
```
kubectl top pod
```

## ConfigMap
- We should no mix code and configuration in same file,lose coupling

## Secrets
- We should only enter the encoded values in secrets both the key value pai should me encoded
- We refer secret and configmap as secretRef and configMapRef simultaneously

##SERVICE
1.Pod to pod communication
2.Load Balancing
* We can communicate with other pods with ip,but the ip changes whenever the pod restarts--so service is used(ephermal)

# DELETE ALL PODS
```
kubectl delete pods --all -n default
```
* Create a service ,attach the pods to it using the selector,selector contains labels
* From another pod hit the service ,using curl <service_name> we can hit the service
* The service gets called and shows output of the attached pods
* can run nslookup of service_name in the main pod, which gives the ip of service

## Types of Services:
1.ClusterIp: default,works internally
2.NodePort: in spec,we should add type: NodePort,we will get Cluster Ip along with node port,the port is opened for all worker nodes
3.LoadBalancer:Only works with cloud providers,Classic,Application LB(Ingress),Network LB
-LB is a external service-nodeport--clusterIp--pod

***
# ReplicaSet
* If we want to have multiple pods ,if we run the same pod.yaml multiple times we get error due to the pod creation with same name.This issue can be solved with replicasets
* When we change the version of the image in replicaset ,the replicaset will not reflect with the changes,it only maintainers the desired state (pod count)

# Deployment
* Rolling update is done with deployments
* Replicaset is subset of Deployment
* Pod is the subset of ReplicaSet which means when we create rs ,pod is also created
* deploymentset > rs >pod
* The selectors present in pod has to be present in service

# ERRIMGPULL
* Not able to pull the image

```
kubectl rollout history deployment<name_of_deployment>
kubectl rollout history deployment<name_of_deployment> --revision=2
kubectl rollout undo deployment/<name_of_deployment>  //to rollback to immediate previous version
kubectl rollout status deployment/<name_of_deployment>
kubectl logs <name of the pod>
```
* targetport cannot be changed,it is the port fixed for each application for nginx it is 80 ,for mysql 3306,but port(service ports) can be changed
* We are running the front end as the non-root user(ec2-user),so we may not access the system ports 0-1024

***
# VOLUMES
1.**EBS**: Elastic Block Storage(similar to hardisk)
- EBS should be present in the same availablity zone as server,it is fast(less latency)
    - OS or DB should be accessed fastly,so EBS is recommended for DB and OS installations
- Installation of Drivers
    -EBS is outside of the cluser,EKS has to connect with EBS,so drivers has to be installed
- EC2 Worker nodes should have permissions to work with EBS Volumes
2.**EFS**: Elastic File System
***
# STATIC AND DYNAMIC PROVISIONING
**Static**: We have to create the disk manually
DRIVER INSTALLATION 
```
kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.41"
```

* EBS are external resources ,if we can treat these voluemes as k8s objects then what ever we do those changes are reflected in EBS also 
1.**PV**-represents or wrapper of physical volume
2.**PVC**
3.**Storage Class**

kid-->mother-->fatner-->wallet
pod-->pvc-->pv-->volume

**ACCESS MODES**
* ReadWriteOnce- At a time only one can read and write,EBS can only be connected to one at a time
* ReadWriteMany - It is for EFS

**LIFECYCLE POLICIES**
1.Retain-Even when we delete pod,pv,pvc data will be available
2.Delete- When pod is deleted ,data will be deleted along with disk
3.Recycle- Data is deleted but disk is available

# PV
1.In static cretae volume and in PV add the volume_id and the size details
# PVC
1.Add the created PV in PVC and keep storageClass as "",in requests you can only have the size less than or equal to the volume created
**If volume is in 1b and the pod  is scheduled in 1a then pod status will be in pending continuously**

***
**NODE SELECTOR**
- nodeselector and volumes will be parallel to containers in manifest
- nodeselector:
    topology.kubernetes.io/zone: us-east-1b
- When we delete pvc and others volume will be released
- In dynamic we will not create the volumes,auto matically volumes get created
- Install the driver befor running th epav and pvc and check
- PV is cluster level ,not based on namespace level

**Static Provisioning Steps**:
1.Install drivers--command
```
kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.41"
```
2.Give permissions to worker nodes  --Security Group--IAM Role--Attach ebs csi permissions
3.create volume
4.create the pv,pvc and clain through pod
5.EC2 and EBS should be in same availability zone

- pod will be created based on the region mentioned in nodeselctor,even th evolume has region bath should be same else the pod will not be created and will get timeout error

# Dynamic Provisioning
Kid-->Mom-->UPI
pod-->PVC-->storageclass
**Storage Class**: this object is responsible for dynamic provisioning,it will create external storage and PV automatically

**Dynamic Provisioning Steps**:
1.Install drivers
2.Give permissions to worker nodes
3.create storage class
```
kubectl get sc //cmd to get starage class
```

- by default the reclaimPolicy is delete so we should explicity define retain
- we should provide the starage class name in dynamic one and no need of volume name

# EBS vs EFS
* EBS is fast compared to EFS
* EBS should be in same AZ where as EFS can be anywhere
* EBS size is fixed ,where as in EFS size will be auto scaled
* EFS is based on NFS(n/w file system protocol)
* EBS and EFS can be useb only when they are mounted to any of the instance
* EBS can have any file system,but for EFS nfs is already fixed so we should use NFS file system for EFS

**EFS installation Steps**:
1.Install drivers
2.Give permissions to worker nodes
3.Create EFS
4.open port 2049 on EFS to allow traffic from worker nodes
5.Create Pv,PVC,pod

* Some access points will be created in our availability zones
* we select the security group which we got in access points and in security groups we will add (nfs 2049 sg attached to instance)
* while creating EFS a volume id is generated that has to be attached in volumeHandle in yaml files
* volume name and storage class in static volume name exists and in dynamic storageclass exists
* We should create EFS and access points will be automatically created
* Access points can be multiple in EFS 
eg: For one project we have backend,frontend,db etc for each we can create differen access points

# StateFulSet vs Deployment
* Deployment is for stateless applications-frontend,backend
* Stateful is for stateful applications like databases,prometheus,grafana
* If master is down then secondary node will act as master ,all the requests in mean time (when master is down)will be stored in a queue and when secondary is up they will reach that DB master and  the app works 
* Statefulset will have **headless** service,deployment will not have headless service
* PV and PVC are mandatory in stateful sets
* pods will be created in orderly manner in staeteful set where as in deployments all pods will be created at once 

**When we hit nslookup on service in deployments we will get clusterip as output**

# What is headless service?
when clusterIp is None (no cluster ip) in service ,then it is considered as HeadLess service

- Instead of creating a PVC resource seperately, we can directly provide in volumeClaimTemplate (statefulset) or can create PVC seperately too
- for every pod their will be unique pv and pvc created
- in stateless when we do nslookup we get the ips of the pods(all the replicas ips will be shown) where as in deployment only one ip is shown

# Normal service,Headless service,stateful set should present in manifest
* in serviceName of stateful set we should mention the headless service name
* env values are overrided during runtime,so we should mention the env values in configmap else we need to rebuild the image
* backend team will share the links if you add them in nginx.conf for connection we have to rebuild the img and should deployagain,if the nginx.conf is added in cofigmap and as it is file i has to attached as a volume and then if any changes in config we can just pull the code and by delete and applying the manifest it works

# AUTOSCALING
1.Vertical Scaling--in the existing server we are increasing the cpu,ram sizes
2.Horizontal Pod scaling(HPA)--no downtime--create another server and add them to LB

# HPA
* minimum,maximum,on what parameter the scaling has to be done ,and which one has to be scaled
- metrics server has to be installed ,this will be installed along with eksctl in kube-sytem which will measure the pods resources
- the resource limits has to be mentioned in pod and in hpa we will mention what has to be autoscaled and min and max details



