# docker-demo
docker demo

## Links
- https://www.youtube.com/watch?v=3c-iBn73dDE
- https://hub.docker.com/
- https://docs.docker.com/


## General
* Docker Image = the actual package, application with configuration.
* Docker Container = start the applicatoin, will create a continer.
* Docker virtualize the applications layer. Much smaller than a VM, much faster.
* Container use the host OS kernal.

## Docker Installation
* Install the yum-utils package (which provides the yum-config-manager utility) and set up the repository.
* To install the latest version.
* Start Docker.
* Verify that the Docker Engine installation is successful by running the hello-world image.
 ~~~
$ sudo yum install -y yum-utils
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
$ sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
$ sudo systemctl start docker
$ sudo docker run hello-world
~~~
## Docker Basic commands

### Container Management
~~~
$ docker create <image> [command]
$ docker run <image> [command]
$ docker start <container>
$ docker stop <container>
$ docker kill <container>
$ docker restart <container>
$ docker pause <container>
$ docker unpause <container>
$ docker rm [-f] <container>
~~~
### Container Inspection
~~~
$ docker ps
$ docker ps -a
$ docker logs [-f] <container>
$ docker top <container>
$ docker diff <container>
$ docker inspect <container>
~~~
### Container Interaction
~~~
$ docker attach <container>
$ docker cp <container:path> <hostpath>|-
$ docker cp <hostpath>|- <container:path>
$ docker export <contaner>
$ docker exec <contaner>
$ docker wait <contaner>
$ docker commit <contaner> <image>
~~~
### Image Management
~~~
$ docker images
$ docker history <image>
$ docker inspect <image>
$ docker tag <image> <tag>
$ docker commit <container> <image>
$ docker import url|- <tag>
$ docker rmi <image>
~~~
### Image Transfer
~~~
$ docker pull <repo[:tag]>
$ docker push <repo[:tag]>
$ docker search <text>
$ docker login
$ docker logout
$ docker save <repo[:tag]>
$ docker load
$ docker-ssh
~~~
### Main Builder
~~~
$ FROM <image>| scratch
$ MAINTAINER <email>
$ COPY <path dst>
$ ADD <src dst>
$ RUN <args>
$ USER <name>
$ WORKDIR <path>
$ CMD <args>
$ ENV <name> <value>
~~~


