# **Docker on Linux overview**

**This is an introduction to Docker on Linux**
**This article was written in July 2022, all the links provided were working at that time** 

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

## **The Docker platform**
Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allows you to run many containers simultaneously on a given host. Containers are lightweight and contain everything needed to run the application, so you do not need to rely on what is currently installed on the host. You can easily share containers while you work, and be sure that everyone you share with gets the same container that works in the same way.

Docker provides tooling and a platform to manage the lifecycle of your containers:

Develop your application and its supporting components using containers.
The container becomes the unit for distributing and testing your application.
When you’re ready, deploy your application into your production environment, as a container or an orchestrated service. This works the same whether your production environment is a local data center, a cloud provider, or a hybrid of the two.

## **What can I use Docker for?**

Fast, consistent delivery of your applications

Docker streamlines the development lifecycle by allowing developers to work in standardized environments using local containers which provide your applications and services. Containers are great for continuous integration and continuous delivery (CI/CD) workflows.

**Consider the following example scenario:**

Your developers write code locally and share their work with their colleagues using Docker containers.
They use Docker to push their applications into a test environment and execute automated and manual tests.
When developers find bugs, they can fix them in the development environment and redeploy them to the test environment for testing and validation.
When testing is complete, getting the fix to the customer is as simple as pushing the updated image to the production environment.

### **Responsive deployment and scaling**

Docker’s container-based platform allows for highly portable workloads. Docker containers can run on a developer’s local laptop, on physical or virtual machines in a data center, on cloud providers, or in a mixture of environments.

Docker’s portability and lightweight nature also make it easy to dynamically manage workloads, scaling up or tearing down applications and services as business needs dictate, in near real time.

### **Running more workloads on the same hardware**

Docker is lightweight and fast. It provides a viable, cost-effective alternative to hypervisor-based virtual machines, so you can use more of your compute capacity to achieve your business goals. Docker is perfect for high density environments and for small and medium deployments where you need to do more with fewer resources.

## **Docker architecture**

Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface. Another Docker client is Docker Compose, that lets you work with applications consisting of a set of containers.

### **Docker Architecture Diagram**
![Architecture](https://user-images.githubusercontent.com/56578405/177573951-4f9fc708-498d-4c0b-beab-ee208ce243c8.png)


### **The Docker daemon**
The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

### **The Docker client**
The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

### **Docker Desktop**
Docker Desktop is an easy-to-install application for your Mac or Windows environment that enables you to build and share containerized applications and microservices. Docker Desktop includes the Docker daemon (dockerd), the Docker client (docker), Docker Compose, Docker Content Trust, Kubernetes, and Credential Helper. For more information, see [Docker Desktop](https://docs.docker.com/desktop/).

### **Docker registries**
A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry.

When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.

### **Docker objects**
When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.

### **Images**
An image is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

### **Containers**
A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.




# **Install Docker Engine on Ubuntu**

[Official Docker Installation Docs](https://docs.docker.com/engine/install/ubuntu/)

`sudo apt-get remove docker docker-engine docker.io containerd runc`

`sudo apt-get update `

` sudo apt-get install ca-certificates curl gnupg lsb-release`

` sudo mkdir -p /etc/apt/keyrings`

` curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`

 `echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

` sudo apt-get update`

 `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin` 

**You can do the addtional steps as well if you want to avoid typing in sudo everytime you use docker.**

` sudo groupadd docker`

` sudo usermod -aG docker $USER`

` newgrp docker `

**Verify Docker installing by running**

`docker run hello-world`

Then type **exit** , to exit from the container. 


# **Using the Docker command line**

##  **[Official Docker Command Line Docs](https://docs.docker.com/engine/reference/commandline/docker/)**

We'll start with most often used docker commands.

## **docker pull**

Purpose: To pull docker images from docker repo or other private repos like Azure etc
Most of your images will be created on top of a base image from the [Docker Hub](https://hub.docker.com/) registry. If no tag is provided, Docker Engine uses the :latest tag as a default. 

![image](https://user-images.githubusercontent.com/56578405/178340393-655963c9-a16f-4b34-9a49-5233a9bd41e2.png)

Docker uses a content-addressable image store, and the image ID is a SHA256 digest covering the image’s configuration and layers. In the example above, debian:jessie and debian:latest have the same image ID because they are actually the same image tagged with different names. Because they are the same image, their layers are stored only once and do not consume extra disk space.

By default, docker pull pulls a single image from the registry. A repository can contain multiple images. To pull all images from a repository, provide the -a (or --all-tags) option when using docker pull

Usage : docker pull [OPTIONS] NAME[:TAG|@DIGEST]

Example

1. docker pull hello-world   --- Pulls hello-world image from docker hub
2. docker pull ubuntu:18.04   --- Pulls ubuntu image from docker hub with ubuntu version as 18.04
3. docker pull ubuntu:16.04   --- Pulls ubuntu  image from docker hub with ubuntu version as 16.04
4. docker pull nvidia/deepstream   --- Pulls deepstream image from nvidia repo
5. docker pull azurecontainer.io/user/testImage:v2   --- Pulls testImage image from docker hub with tag as v2

Tags are necessary when multiple images with same name exists. Think of it as version control.


## **docker run**

Purpose : Run a command in a new container

Usage : docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Some Commonly used options for docker run are : 

* --cpus              |        Number of CPUs
* --detach , -d       |        Run container in background and print container ID
* --device            |        Add a host device to the container
* --entrypoint        |        Overwrite the default ENTRYPOINT of the image
* --env , -e          |        Set environment variables
* --expose            |        Expose a port or a range of ports
* --gpus              |        GPU devices to add to the container ('all' to pass all GPUs) **(Install nvidia-docker if required)**
* --hostname , -h     |        Container host name
* --interactive , -i  |        Keep STDIN open even if not attached
* --ip                |        IPv4 address (e.g., 172.30.100.104)
* --link              |        Add link to another container
* --mac-address       |        Container MAC address (e.g., 92:d0:c6:0a:29:33)
* --memory , -m       |        Memory limit
* --mount             |        Attach a filesystem mount to the container
* --name              |        Assign a name to the container
* --network           |        Connect a container to a network
* --publish , -p      |        Publish a container's port(s) to the host
* --rm                |        Automatically remove the container when it exits
* --shm-size	      |        Size of /dev/shm (Shared memory)
* --user , -u         |        Username or UID (format: <name|uid>[:<group|gid>])
* --volume , -v       |        Bind mount a volume
* --workdir , -w      |        Working directory inside the container

Some examples with docker run command

> 1. docker run hello-world

> You'll get something similar on your screen. So the default behaviour of a docker container is to exit if there is nothing else to do. This is what's happening here. it goes into the hello-world image, runs the program and exits it.

> ![image](https://user-images.githubusercontent.com/56578405/177619493-01e61245-427e-4294-9425-b6a14c0c0ed0.png)

> 2. docker run ubuntu:18.04

> This will pull the ubuntu:18.04 docker image from the docker repo, run it and immediately exit as there is nothing waiting to be done.

> 3. docker run -it ubuntu:18.04 bash

> This time it'll go into the container and keep waiting in the terminal. The -it parameter is for telling the container that we'll be interacting with it and bash is for telling the container that we'll be interacting with bash shell. Type "exit" to exit from the contianer.

> 4. docker run -it --rm ubuntu:18.04 bash

> This will remove the container as we exit from it. In above cases, it'll just stop the container. Run the command "docker ps -a" to see the stopped containers.

> 5. docker run -w /path/to/dir/ -it  ubuntu:18.04 bash

> The -w lets the command being executed inside directory given, here /path/to/dir/. If the path does not exist it is created inside the container.

> 6. docker run -v /path/on/host:/path/in/container -it  ubuntu:18.04 bash
> This mounts (or syncs) the host directory with the path in the container.

> 7. docker run-it --mount type=bind,src=/hostPath,dst=/containerPath ubuntu:18.04 bash
> This is similar to -v in mounting paths.

Go through the official docs for more examples **[Official Docker Command Line Docs](https://docs.docker.com/engine/reference/commandline/run/)** .


## **docker login**

Log in to a Docker registry

Usage:
By default it's docker hub/repo : docker login
If different repo like Azure Container registry : docker login <repo name.acr.io>
Then enter username and password


## **docker logout**

Log out from a Docker registry
Usage:
Docker Hub: docker logout
Other repository: docker logout <server name>


## **docker image**
For managing images. Difeerent commands are available for images. Full list here [Docker image command official docs](https://docs.docker.com/engine/reference/commandline/image/)

one of the most commonly used command is:

docker image ls

List all available images

## **docker commit**

Create a new image from a container’s changes. After running a container , suppose you install few things in it, and now you want to save it permanently. For this pupose, we use docekr commit to generate a new image.

Usage: Fisrt run **docker ps** to find the name/container ID of the container you want to commit
then run the command ,
`docker commit <container ID/name> <new image name>:<tag>`

## **docker cp**

Copy files/folders between a container and the local filesystem

Usage: `docker cp CONTAINER_NAME:SRC_PATH DEST_PATH_ON_HOST`
`docker cp SRC_PATH_ON_HOST CONTAINER_NAME:DEST_PATH`

## **docker exec**

Run a command in a running container / interact with a container running in detached mode.

Usage:
docker exec -it <container name> bash
docker exec <container name> <command>


## **docker info**

Display system-wide information


## **docker inspect**

Return low-level information on Docker objects

Usage:
docker inspect <network/image/container name>


## **docker kill**

Kill one or more running containers

Usage:
docker kill <container name>


## **docker load**

Load an image from a tar archive or STDIN

Usage:
docker load --input fedora.tar
docker load < busybox.tar.gz


## **docker ps**

List containers currently running / stopped

Usage:
Running containers only : docker ps 
Running and Stopped containers : docker ps -a


## **docker push**

Push an image or a repository to a registry

Usage:
docker push <reponame.image name:tag>


## **docker rm**

Remove one or more containers

Usage:
docker rm <container name>


## **docker rmi**

Remove one or more images. Images can removed only if there are no dependent containers of that image. Remove the containers of the image first, then remove the image.

Usage:
docker rmi <image name>


## **docker save**

Save one or more images to a tar archive.

Usage:
docker save -o <output tar file > <image name:tag>
Example : docker save -o fedora-all.tar fedora

Save an image to a tar.gz file using gzip
You can use gzip to save the image file and make the backup smaller.
docker save myimage:latest | gzip > myimage_latest.tar.gz



## **docker tag**

Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

Usage:
docker tag SOURCE_IMAGE_NAME:TAG TARGET_IMAGE_NAME:TAG


Some real world examples of docker commands:

