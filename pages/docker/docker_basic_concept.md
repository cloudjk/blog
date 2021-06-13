---
title: Docker Basic Concept
sidebar: mydoc_sidebar
permalink: docker_basic_concept.html
folder: docker
---
### Containers vs Virtual Machine

{% include image.html file="container-vm.png" %}

### Container vs Image

1. Image is a package or a template used to create one or more containers.
2. Containers are running instances of images that are isolated and have their own environments and set of processes.
3. Docker file contains a requirement guide to create an image.

### Commands

```bash
docker run nginx // run an instance of the nginx locally but image is not present, it will pull the image down from the docker hub

docker ps // list all running containers

docker ps -a // list all running and stopped or exited containers

docker stop :CONTAINER ID OR :NAMES // stop container

docker rm silly_sammet // remove a stopped or exited container permanently

docker images // list all availabe images

docker rmi nginx // remove image. !! No containers are running off of that image. Stop and delete all dependant containers before removeing image.

docker pull nginx // only pull the image and not run the container

docker run ubuntu sleep 5 // install locally or pull down the image from docker hub and wait 5 seconds then exits

docker run ubuntu sleep 100
docker exec :NAMES cat /etc/hosts // execute a command on a running container
```

### Reason running **docker run ubuntu** exits in a sec

- Unlike virtual machine, containers are not meant to host an operating system. Containers are meant to run a specific task or process such as
to host an instance of web server or application server or database. Once the task is complete the container exits.
- If the web service inside the container is stopped or crash then the container exits.
- Ubuntu is just an image of an operating system that is used as the base image for other applications. There is no process or application
running in it by default.

### Run - attach & detach

- Run in forground

```bash
docker run kode/webapp # To stop Ctrl + C
```

-  Run in background

```bash
docker run -d kode/webapp # back to the prompt immediately
```

- Attach back to the running container

```bash
docker attach a043d
```