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
Install the yum-utils package (which provides the yum-config-manager utility) and set up the repository.
To install the latest version, run:
Start Docker.
Verify that the Docker Engine installation is successful by running the hello-world image.
 ~~~
$ sudo yum install -y yum-utils
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
$ sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
$ sudo systemctl start docker
$ sudo docker run hello-world
~~~ 


