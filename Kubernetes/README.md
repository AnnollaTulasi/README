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

**REQUESTS vs LIMITS **
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

* Create a service ,attach the pods to it using the selector,selector contains labels
* From another pod hit the service ,using curl <service_name> we can hit the service
* The service gets called and shows output of the attached pods
* can run nslookup of service_name in the main pod, which gives the ip of service

## Types of Services:
1.ClusterIp: default,works internally
2.NodePort: in spec,we should add type: NodePort,we will get Cluster Ip along with node port
3.LoadBalancer:Only works with cloud providers,Classic,Application LB(Ingress),Network LB
-LB is a external service-nodeport--clusterIp--pod





