**VPC-Virtual Private cloud**
- it is a isolated project space where we csn create services or project
- we will have full control and access to that space
- VPC has CIDR number(Classless inter Domain routing)
- internet Gateway-modem for internet- attach to VPC
- subnets
- no outside person should access database- private subnet
- frontend has to be accessed by any user - public subnet
- routes are in b/w subnets- only when routes are available you can reach the application
- 10.0.0.0/16 16 bits are reserved 10.0.0.1--10.0.0.255 and 10.0.1.0 --10.0.255.0 total 256*256 possibilities
- for 10.0.0.0/16 we can create 65536 servers
- for subnet also we have the CIDR
- for each subnet we will have separate route tables
- all the subnets can communicate internally
- internet is not inside the network so we should add this route to route table
**Difference between public subnet and private subnet**
- public will have the route to Internet gateway
- private will not have route to Internet gateway
**NAT Geeway**
-  if you want to egress internet to the servers in private subnet,nat gateway should be created in public subnets and provide routes to private subnets
- elastic or static ip and it has some cost as we are requesting for some static ip
- for nat gateway elastic ip is mandatory
- by default public ip is set as false we should add that option for public subnets in vpc(map_public_ip_on_launch)
- slice is the method which takes the continous output at mentioned indices
- we get output when we apply and when the resources are created
- internet gatewayy is responsible for internet in public subnet
- for natgateway elastic ip is mandatory aswell it should have internetgateway only then public subnet gets internet connection
**Asociations**
- route tables has to be associated with subnets
**VPC Peering**
- Generally VPCs will not communicate with each other,inorder to make them communicate the VPC should be attached via peering
1. VPC 1 cidr should be different ffrom VPC 2 cidr
2. routes should be present between VPCs route tables
