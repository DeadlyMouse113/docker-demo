# docker-demo
docker demo

This demo is done on Rocky Linux 9 in a virtual lab.

## Demo App
- https://gitlab.com/nanuchi/techworld-js-docker-demo-app

## Links
- https://www.youtube.com/watch?v=3c-iBn73dDE
- https://hub.docker.com/
- https://docs.docker.com/
- https://dockerlabs.collabnix.com/docker/cheatsheet/

## General
* Docker Image = the actual package, application with configuration.
* Docker Container = start the applicatoin, will create a continer.
* Docker virtualize the applications layer. Much smaller than a VM, much faster.
* Container use the host OS kernal.
* Docker Compose takes care of creating a common Network.

### Conatiner Port vs Host Port
* Multiple containers can run on your host machine.
* Your laptop has only certain ports available.
* Conflict when same port on host machine.
* You need port binding between host and container.

### Persistent Volume
* Folder in physical host file system is mounted into the virual file system of Docker.
* Data written in the virtual file system is replicated to the host file system adn vice versa.

#### 3 Volume types
* Host Volumes
* Anonymouse Volumes
* Named Volumes (best fit in production)

## Docker Installation
* Install the yum-utils package (which provides the yum-config-manager utility) and set up the repository.
* To install the latest version.
* Start Docker.
* Verify that the Docker Engine installation is successful by running the hello-world image.
 ~~~
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl start docker
sudo docker run hello-world
~~~
## Docker Demo Project Steps
### With docker
1. Pull Images from Docker Hub
~~~
docker image pull mongo
docker image pull mongo-express
docker images
~~~
2. Create Docker network
~~~
docker network create mongo-network
~~~
3. Start MongoDb
~~~
docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
~~~  
4. Start Mongo-Express
~~~ 
docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb -e ME_CONFIG_MONGODB_URL=mongodb://admin:pass@192.168.220.120:27017/db?ssl=false mongo-express  
~~~
*** 
Note: Change the ip of the ME_CONFIG_MONGODB_URL to the ip of your instance or to 'localhost'.
***
5. Check mongodb and mongo-express from a browser (disable firewall or open correct port on host if needed)
~~~  
docker exec -it mongodb mongosh
db.runCommand({hello:1})

sudo systemctl disable firewalld
http://<localhost - your ip>:8081
~~~
6. create my-db db and users collection in mongo-express
![image](https://github.com/DeadlyMouse113/docker-demo/assets/121127124/68843ce0-9c31-4731-aa3d-b88c58a333de)

7. On the Rocky Instance, install git and clone the repository with the app.
~~~
sudo yum install git -y
git clone <this repo>
~~~
7. Install prerequisites and nodjes on Rocky Linux
(I have all modules under my root directory for this demo, not best practice for production)
~~~
sudo dnf install nodejs -y
node -v

npm install express
npm install path
npm install fs
npm install mongodb
npm install body parser
~~~
8. Start de application
~~~
node server.js
~~~
9. Access you nodejs application UI from browser
http://<localhost - ip>:3000
Note: check following lines in server.js
~~~
// use when starting application locally
let mongoUrlLocal = "mongodb://admin:password@192.168.220.120:27017";
~~~
### With Docker Compose






### Flow
![image](https://github.com/DeadlyMouse113/docker-demo/assets/121127124/0bf831ea-670c-4ff0-a4b4-def84eb8d1f1)
### Software Development
![image](https://github.com/DeadlyMouse113/docker-demo/assets/121127124/3809ab43-d5eb-4e76-b52e-641430144137)
#### With Docker
![image](https://github.com/DeadlyMouse113/docker-demo/assets/121127124/2eee0ff1-eaed-461f-b4f1-fa698fcc55f8)
#### With Docker Compose
![image](https://github.com/DeadlyMouse113/docker-demo/assets/121127124/3afdff04-d7e1-4ec4-93cd-6a0378921e2f)

## Docker Basic commands
### Container Management
~~~
 docker create <image> [command]
 docker run <image> [command]
 docker start <container>
 docker stop <container>
 docker kill <container>
 docker restart <container>
 docker pause <container>
 docker unpause <container>
 docker rm [-f] <container>
~~~
### Container Inspection
~~~
 docker ps
 docker ps -a
 docker logs [-f] <container>
 docker top <container>
 docker diff <container>
 docker inspect <container>
~~~
### Container Interaction
~~~
 docker attach <container>
 docker cp <container:path> <hostpath>|-
 docker cp <hostpath>|- <container:path>
 docker export <contaner>
 docker exec <contaner>
 docker wait <contaner>
 docker commit <contaner> <image>
~~~
### Image Management
~~~
 docker images
 docker history <image>
 docker inspect <image>
 docker tag <image> <tag>
 docker commit <container> <image>
 docker import url|- <tag>
 docker rmi <image>
~~~
### Image Transfer
~~~
 docker pull <repo[:tag]>
 docker push <repo[:tag]>
 docker search <text>
 docker login
 docker logout
 docker save <repo[:tag]>
 docker load
 docker-ssh
~~~
### Main Builder
~~~
 FROM <image>| scratch
 MAINTAINER <email>
 COPY <path dst>
 ADD <src dst>
 RUN <args>
 USER <name>
 WORKDIR <path>
 CMD <args>
 ENV <name> <value>
~~~




