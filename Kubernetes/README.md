*Kubernetes*
-When the containers increases it is difficult to manage them,so for orchestration purpose kubernetes came into picture
-eksctl is used to create ,update and delete clusters
-images are already created and how to interact with images is discuussed in manifest files
-EKS is useful fr creating the control plane(master) and in the nodegroup(nodes) we should attach the ec2 instances
-kubectl is to interact with the cluster
-We cannot simply connect to cluster,authentication is required

Authentication to cluster
-aws configure (aws cli)
-IAM Role

Kuberneters Cluster Setup
1.create one linux server as workstation
2.install docker to build images
3.Run aws configure to provide authentication
4.eksctl to create cluster
5.kubectl to interact with cluster

#Instances
-Ondemand : creating server on spot ,costly
-Reserved : booking/reserving the server before as it is planed before
-Spot : when the desired capavity is not used they will provided the resources on discounts--Availablity is not guaranteed--with 2 min notice the hardware will be removed when the aws itself requires
*Spot is not used for PROD only for testing we can use

CLUSTER CREATION CMD
eksctl create cluster --config-file=eks.yaml
eksctl delete cluster --config-file=eks.yaml

-Isolation in kubernetes is achieved by namespace
-Workstation is the common server which is in betwwn our system and kubernetes cluster
-the kubernetes manifest file are cloned into the server and when we use kubectl commands and apply the manifest file it is applied into the cluster

#Difference b/w create and apply
create throws error if already the manifest is created
-apply will create only when the manifest file is not created else just shows warning instead of throwing error

docker-->image-->container
k8s-->image-->pod

POD Vs CONTAINER
*Pod is the smallest deployable component,Pod can have one or many containers

#CRASHLOOPBACKFF
*When a image is runned ,if it is not started restarts will happen and even after restart if the container is not up then we get CRASHLOOPBACKOFF error

#The container should run infinite time so that it will not exists and only then the application is available to the outside world
* For nginx the code to run infinitely is present as the image is already create by different people
*But for almalinux we should create the cmd to run the conainer infinitely

* If we have 2 containers in the yaml file we can enter different container by the below command
kubecl exec -it <pod_name> -c <container_name> -- bash

* All containers in the pod share the same ip and storage
* Logs of a pod are available until it is up
*ELK is to store logs,even if the server is deleed,we cannot have logs
*sidecar container access the storage of the server and pushes the logs outside(ELK)

#LAbels vs Annotations
*Labels are for selecting internal  resources
*annotations are for selecting external  resources and can have special characters like :// (links)



