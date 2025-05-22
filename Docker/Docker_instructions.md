**DOCKERFILE**
- to create custom images dockerfile is used
- Service should run continuosly in order to access
- if we don't give any command bash is considered as default and in that their isno cmd which runs the conatainers continuously so it exits
- systemctl will not work in dockerfiles ,systemd in server cannot be accessd by container
- No CPU,RAM are provided for containers,allthe containers uses the CPU,RAM of the server
- When we use exec cmd,we will have root access,then from container it is possible to access the resources of the server which is not good,so it is better to not access the containers with root access privileges

**INSTRUCTIONS**
- RUN is used to install packages,configurations on top of base os,executes while building the image
- CMD command is used to run the imaage continuously
- COPY to copy the file in our local to the server
- ADD
- LABEL -adds metadata ,they are key value pairs
- EXPOSE - gives port informations//metadata related only
- in docker inspect we can check the labels added and port exposed details
- ENV are environment variables and can access inside containers
- after entering the container by exec command if we check for env these variables will be available and these can be useed inside code
- ENTRYPOINT - not overriden
- USER - when we enter the container we will have root access,if we use USER then the root access will be removed ,in containers sudo option is not available so after changing from root you cannot have root privilages for normal user
- WORKDDIR - instead of cd it has to be used and cd will not work in dockerfile it will always point to root folder / . If dir is not present it will create the directory
- ONBUILD - will execute when others use our image as their base image and it enforces to meet the contidions

```
FROM <base_os>:<version>
RUN dnf install nginx -y //to install any thing on top on base os
RUN rm -rf /usr/share/nginx/html/inde.html
COPY index.html /usr/share/nginx/html/inde.html
ADD sample.tar /tmp //untar and saves in tmp
LABEL project="expense"\
      environment="dev"\
      component="frontend"
ENV course="devops"\
    trainee="tulasi"
RUN usersdd expense
ONBUILD COPY index.html /usr/share/nginx/html  //the index.html file should be present when they are using our image
USER expense
CMD ["nginx", "-g", "daemon off;"] //executable format
```

```
docker build -t <image_name>:<version> .  // will build and save in local registry
docker build -t <dockerhub_username>/<image_name>:<version> . //to store in dockerhub
docker login -u <username> // to login docker hub
docker tag <name> <replaced_name> //to chage the name of already built one
docker tag from:1.0.0 annollatulasi/from:1.0.0
docker push <image_name>
docker images -f "LABEL=<Key=value>"
```

**RUN Vs CMD**
- Run executes while image building
- CMD executes while container creation

**COPY vs ADD**
- both copes the files to containers/images
- if we download something from internet it might not have the read permissions,so we should add the permissions
- Add has 2 more fuctionalities
1. copying from internet to image
2. extracts tar file into image - it will untar and will store in container

**CMD vs ENTRYPOINT**
- we can override the command givven in CMD
- We cannot override from ENTRYPOINT
- command is appended in ENTRYPOINT
- docker run cmd:1.0.0 ping facebook.com //way to override
- In ENTRYPOINT cmd is defined and in CMD inputs are given for better usage of both cmds
- Only one CMD and ENTRYPOINT should be used is dockerfile
```
CMD ["ping", "google.com"]
ENTRYPOINT ["ping", "google.com"]
```
- docker run cmd:1.0.0 facebook.com
```
CMD ["google.com"]
ENTRYPOINT ["ping"]
```

**ARG vs ENV**
- ENV can be used both while building the image and in container
- ARG can only be used while building the image
- ARG can be added in first line instead of FROM to get the version details
- It will work only till FROM ,after that you cannot access after FROM cmd
```
docker build -t <name>:<version>  --no-cache --build-arg USERNAME=Tulasi //to override the ARGS,--no-cache for better o/p

ARG USERNAME
RUN echo "Hello $USERNAME"
```

**How can we use ARG inside container**
- We cannot actually use the ARG in container
- but we get the value of arg and set it to ENV to use inside container
```
ARG USERNAME=Tulasi
ENV USERNAME=$USERNAME
```

===============================================================
**NETWORK**
- In default network the containers cannot communicate with each other,we have to create some network and in that the containers are to be created inorder to communicate
- host and bridge are the types of networks
- Usually in images all configuration are also removed ,we have to check and add the required configurations
```
docker network create <networkname>
docker network disconnect default mysql
docker network connect <networkname> mysql
docker run -d --name backend --network expense backend:1.0.0
```