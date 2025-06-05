**K8s Architecture**
- control plane(master) and Worker node
**Control Plane**
- **API server**: first component to receive request from client and checks authentication and authorization and forwards to scheduler
- kubectl command reches API server and then API server deals with other components
- **Scheduler** - takes decision about where to schedule the pods/workloads
- affinity (node ,pod),taints and toleration 
- **Control Manager** -node control,replica control,continuaously watches and manages the desired number of resources are available
- node controller mains the node count
- Service Account controller,whenever we create namespace a DEFAULT service account is created
- **etcd** - database to the k8s cluster,it stores all the configuration details and all in key value pair based
- **cloud-control manager** : responsible to integrate eks cluster with other cloud services like IAM,LB,ingress

=================================================================
**WORKER node**
- **kubelet** : responsible for connecting master and worker node
- it gets pod spec from master nodde and make sure the pods run on the nodes
- **kube -proxy**: like DNS to the pods,it provides the network rules on how to forward request through workloads like service to pods(pod to pod communication)
- **container runtime**: reponsible to run image to container
- **add-ons**: vpc-cni,kube-dns,metrics-server,ebs,efs