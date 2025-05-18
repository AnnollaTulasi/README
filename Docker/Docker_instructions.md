**DOCKERFILE**
- to create custom images dockerfile is used
- Service should run continuosly in order to access
- if wwe don't give any command bash is considered as default and in that their isno cmd which runs the conatainers continuously so it exits
- systemctl will not work in dockerfiles ,systemd in server cannot be accessd by container

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
- ENTRYPOINT

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