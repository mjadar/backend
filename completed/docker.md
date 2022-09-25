# DOCKER TUTORIAL

## What is a container ?

- a way to package applications with all the necessary dependencies and configuration;
- portable artifact, easily shared and moved around
- makes development and deployment more efficient.

## where do containers live ?

- container repository
- private repositories
- public repositories for Docker (Docker Hub)

## How apps developed before containers ?

- install dependencies on local directly
- installation process different on each OS environment
- many steps where something could go wrong

## How apps developed after containers ?

- do not have to install any of the services directly on the OS.
- own isolated environment
- packaged with all needed configuration

## Technically, What is a container ?

- layers of images
- mostly linux base image, (alpine) because small in size
- then the application image is on top
- ==> linux base image < application image

## Docker Image vs Docker container :

- `Docker image` = the actual package of the app with configuration, script and dependencies.
- `Docker container` = when we pull the image, and the application starts, that creates the container.
- Container is a running environment for IMAGE.

## Docker vs Virtual Machine :

- they are both virtualization tools
- **How Docker works on Operating system :**
  - OS have 2 layers [Hardware, OS Kernel (layer1), Application (layer2)]
  - Kernel communicates with hardware
  - applications run on kernel layer
  - [DOCKER] virtualize the application layer, and use the kernel of the host.
  - [VMS] virtiualizes the complete OS, it doesn't use my OS but it creates it s own
- Docker image is much smaller.
- Docker containers start and run much faster.
- VM of any OS can run on any OS host.

## Commands :

- `docker pull postgres:9.6` // to pull image docker

- `docker run redis` //create container of image or pull + run if not found locally
- `docker run -d redis` //run docker container in detach mode (in background)
- `docker run -p 6000:6379 --name redis-container redis` //bind HOST_PORT to CONTAINER_PORT

- `docker stop CONTAINER_ID`
- `docker start CONTAINER_ID`
- `docker ps -a` //lists running and stopped containers

- `docker exec -it CONTAINER_ID /bin/bash` //will open terminal of specified container
- `docker exec -it CONTAINER_NAME /bin/bash` // open terminal of specified container name

- `docker rm CONTAINER_ID` #to delete a container

## Docker Network

- `docker network create mongo-network` // create isolated network
- `docker run -d -p HOST_PORT:CONTAINER_PORT --name CONTAINER_NAME --net CONTAINER_NETWORK`

```
# create docker network
 docker network cerate mongo-network

# start mongodb
 docker run d \
 -p 27017:27017 \
 -e MONGO_INITDB_ROOT_USERNAME=admin \
 -e MONGO_INITDB_ROOT_PASSWORD=password \
 --net mngo-network \
 --name mongodb \
 mongo

# start mong-express
 docker run -d \
 -p 8081:8081 \
 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
 -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
 -e ME_CONFIG_MONGODB_SERVER=mongodb \
 --net mongo-network \
 --name mongo-express \
 mongo-express
```

## Docker compose

- manage docker containers
- Docker compose takes care of creating a common network

```
# save file under mongo.yaml
# be aware of indentation it is important

version: '3'
services:
  mongodb:
    image: mongo
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password
  mongo-express:
    image: mongo-express
    ports:
      - 8080:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_SERVER=mongodb
```

- `docker-compose -f mongo.yaml up` // to start containers
- `docker-compose -f mongo.yaml down` // to stop and remove containers

## Dockerfile

```
# save under Dockerfile

From node # install node on container

ENV MONGO_DB_USERNAME=admin # set environment variables

RUN mkdir -p /home/app  # executes any linux command, are run inside of the container environment

COPY . /home/app # executes on the host machine

CMD ["node", "server.js"] # executes an entrypoint linux command, you can execute one CMD but multiple RUN commands
```

- in order to build image with Dockerfile, you should give it a tag, and location of Dockerfile; using this command :
  - `Docker build -t my-app:1.0 .`
- then Jenkins builds image from Dockerfile
- When you adjust Dockerfile, you must rebuild the image

- `docker rmi IMAGE_ID` # to delete an image

## Deploy app

- in Dockerfile add section for my-app image

## Docker volumes

- it is used for data persistence
- the virtual file systems remove data when restarting or deleting the container
- ** The solution ** is we plug the physical Host file system /home/mount/data
- Technically, a folder in physical host file system is mounted into the virtual file system of Docker

- 3 volume types :
  - [HOST_VOLUMES] = you decide where on the host file system the reference is made
    - `docker run -v /home/mount/data:/var/lib/mysql/data`
  - [ANONYMOUS_VOLUME] = for each container a folder is generated that gets mounted
    - `docker run -v /var/lib/mysql/data`
  - [NAMED_VOLUMES] = it create named volumes, and you can reference the volume by name. It should be used in production.
    - `docker run -v name:/var/lib/mysql/data`

```
# save file under mongo-docker-compose.yaml

version: '3'
services:
  mongodb:
    image: mongo
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password
    volumes:
      - mongo-data:/data/db #path differs for each database
  mongo-express:
    image: mongo-express
    ports:
      - 8080:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_SERVER=mongodb
volumes:
  mongo-data:
    driver: local
```

- `mongo-data:/data/db` ==> means all data in container under location /data/db will get replicated under the named location in the host file system referenced by mongo-data.
