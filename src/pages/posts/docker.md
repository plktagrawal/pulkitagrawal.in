# Docker

In this post we will learn Docker.

<iframe width="560" height="315" src="https://www.youtube.com/embed/fqMOX6JJhGo?si=wnLMtcEh3OoeXFOH" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## What is Docker

It is a tool on top of which you can run an application. Docker provides a standard interface for applications irrespective of the operating system (and environment) underneath, so the application can run on any machine irrespective of the differences in the operating environment.

## Installation

Install docker desktop using the instructions on docker website.

## Core Concepts

1. Images - a copy of the application.
2. Containers - an instance of the image that can be run. The container runs only as long as the process inside of it is running. It exits as soon the process stops.
3. Volume -
4. Registry - a place where images can be stored and retrieved.
5. Tags - tags are used to identify versions of images

## Commands

1. Check Version
   `docker version`

2. Pull and run an image
   `docker run <image name:tag>`

3. Just pull the image from docker hub, without running it
   `docker pull <image name>`
   For example:
   `docker pull nginx`

4. List runnning containers
   `docker ps`

5. List all containers, running or not
   `docker ps -a`

6. Stop running Docker
   `docker stop <conatiner name>`

7. Delete stopped container
   `docker rm <conatiner name>`

8. List all images
   `docker images`

9. Remove an image
   `docker rmi <image name>`

10. Run a docker container and execute a command inside it
    `docker run ubuntu sleep 5`

11. Run a command inside and already running container
    `docker exec <container name> <command>`

For example:
`docker exec silly-mammoth cat /etc/hosts`
This command will list the contents of the etc/hosts file

12. ### Detach flag
runs the container in the background
    `docker run <container name> -d`

13. Attach command - brings the container running in the background to the terminal foreground
    `docker attach <container name>`

14. ### Interctive mode
    The `-it` flag turns on the the interactive mode. This way you can provide inputs to the process running inside the docker container from your terminal

`docker run -it <container name>`

15. ### PORT mapping
Use the `-p` tag
    `docker run -p <host port>:<docker container port> <docker container name>`

For example:
`docker run -p 80:3000 run nginx`

Here 80 is the port that can be visited on the browser. 3000 is the port that is inside the docker container.

16. ### Data Persistence
    Each docker conatiner has its own filesystem. If you store data inside a docker conatiner, it will be lost when the container is deleted.

To persist data, map a folder on your local machine to a folder inside the docker container with the `-v` tag. Any data stored in that docker folder will then be actually stored in the mapped folder outside of the conatiner.

`docker run -v <dirpath on server>:<dirpath in container> <container name>`

For example:

```shell
# Run mysql container while mapping 
# /opt/datadir on the server to 
# the /var/lib/mysql folder inside the container
docker run -v /opt/datadir:/var/lib/mysql mysql
```

17. ### Inspect a container
With the `inspect` command you can see details about the container in a JSON format.
`docker inspect <container name>`

18. ### View Logs of the container
Use the `logs` command to view the logs for a particular container.
`docker logs <container name>`

## Environment Variables
You can use the `-e` tag to set environment variable inside a container.

`docker run -e SECRET_KET=kjbhvervubwlurbvwlureb django`

The `inspect` command will show the existing environment variables for a container. Look in the "Config" section of the JSON that is returned by the inspect command.

## Docker Images

###  Create your own docker images
The general steps for building a project are:
1. Select an OS
2. Update the `apt` repo
3. Install dependencies using `apt`
4. Install python dependencies using `pip`
5. Copy source code into the /opt folder
6. Run the application using the appropriate command (`python manage.py runserver`)

All of the above are done in the `Dockerfile`. Then the dockerfile can be run using the `build` command as follows:
`docker build <Dockerfile path> -t <tagname>`

### Push the image to a registry
Use the `push` command.

`docker push <image name>`

### Dockerfile

```docker
# 1. Select an OS
FROM Ubuntu

2. Update the `apt` repo
RUN apt-get update

3. Install dependencies using `apt`
RUN apt-get install python

4. Install python dependencies using `pip`
RUN pip install django django-ninja

5. Copy source code into the /opt folder
COPY . /opt/source-code

6. Run the application using the appropriate command (`python manage.py runserver`)
# We can also have an entrypoint here
CMD ["python", "manage.py" "runserver"]
```

### Layered Architecture
Each docker image is built in layers. One layer for every line in the `Dockerfile`.

Use the `history` command to see all the layers in an image.

`docker history <image name>`

## Networking
Docker makes three tpes of networks:

1. Bridge - the internal network. All containers can network with other containers in the same host but not with the outside world. It is the *Default* option.
`docker run nginx`

2. None
Creates totally isolated containers -- not connected to each other or to the host network.
`docker run nginx --network=none`

3. Host
Containers are assigened a port on the host network so they can communicate with the outside world.
`docker run nginx --network=host`

### List all existing networks
`docker network ls`

### Create You Own Network
`docker network create \
   --`
