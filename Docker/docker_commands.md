- when frontend and backend are deployed together,if any changesa are made in any of them ,whole application has to be rebuild and redeployed
- later backend and frontend are distinguished from each other ,but in monolithic only single programming language is used and all the components in backend has to be tested when any changes are done
- in microservices all the components are in different servers and through ALB(by urls) the request will reach to different servers and output is retrieved
- client and server can use any language ,we just need to get the date and display it
- business impact will be less in microservices as all the components will work even if one of the component is down
- when application size decreases,the size of resources should also be reduced

**VM vs Containers**
1.cost
2.boot time is more in VM
3.Vm size is big
4.Vm blocks the resources
5.Autoscaling of VM takes time (boot time is more)
6.Containers are more portable


```
systemctl start docker
systemctl enable docker
systemctl status docker
```
- only with sudo access docker commands execute
- docker group is created while installing
- we should add the ec2-user to the dockergroup
```
usermod -aG docker ec2-user
```
- VM-->AMI--->Instance
- Docker-->Image--->Container
- we should run the image to have the container,by pulling image nothing will happen
- in base minimum os ping,vim and some main commands will not work,we have to install them and work
```
docker ps //running containers
docker ps -a // all containers
docker pull image //pulls the image from docker hub too local regidtry
docker create <image_name> //creates
docker start <container_id> //to run the container
docker rm <container_id> //to remove container
docker rm -f  <container_id> //to remove the running container,in docker ps these will not be visible
docker rmi <image_name/id> //to remove images
docker images -a -q // to get the ids of all images
docker run <image_name> // pull+create+start
docker run  -p <host_port>:<container_port> -d <image_name/id>  // to run in background
docker exec -it <id> bash
docker logs <container_id>
docker inspect <container_id>
```

