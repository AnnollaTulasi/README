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