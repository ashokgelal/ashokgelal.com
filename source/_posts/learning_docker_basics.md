---
title: Learning Docker - Basics
date: 2017-02-17 00:01:38
tags:
- docker
- sysadmin
- virtualization
---

Currently I'm learning Docker using the excellent [Shipping Docker](https://shippingdocker.com) video series. I just wanted to dump everything I've learned through the end of each chapter for my future self here.

<!--more-->

### What is Docker?

Unfortunately, Shipping Docker doesn't go through actually defining what docker actually is -- it gets right into the action so I've no complaints. Here is the best definition I found from Docker's Wikipedia page:

> Docker automates the deployment of applications insider software containers. It wraps up a piece of software in a complete filesystem that contains everything it needs to run. This guarantees that it will always run the same regardless of the environment it is running in.

* Three docker commands:

1. `docker` - manages the lifecycle of docker containers
2. `docker-compose` - coordinates the use of multiple containers
3. `docker-machine` - spin up servers and control remotely

* Relationship between images and containers

	base image -> running container -> stopped container

* Some `docker` command examples:

```bash
$ docker ps
	# check for running containers
```

```bash
$ docker ps -a
	# check for existing containers, running or not
```

```bash
$ docker images
	# view local images
```

* Creating and running an image

```bash
$ docker run ubuntu:16.10 ls -lah
	# 1. if ubuntu:16.10 doesn't exist it downloads the image
	# 2. create a new container based on ubuntu:16.10
	# 3. run ls -lah command in the container
	# 4. stop the container
```

* Inspecting a container

```bash
$ docker inspect container_name_or_id | jq
	# jq is a different command for formatting a json string in the terminal downloadable using brew
```

* Removing a container

```bash
$ docker rm container_id
```

* Removing all existing containers

```bash
$ docker rm $(docker ps -aq)
	# docker ps -aq just returns a list of container ids
```

* To automatically clean after running - just add a `--rm` flag:

```bash
$ docker run --rm ubuntu:16.10 ls -lah
```

* Removing an image use `rmi`:

```bash
docker rmi ubuntu:16.10
```

* Interacting with the containers

```bash
$ docker run -i -t ubuntu:16.10 bash
	# -i => interactive
	# -t => allocate a pseudo-TTY
	# you can combine -i -t to -it
```

* Starting/ Stopping an existing container

```bash
$ docker start container_id
	# container is running but isn't interactive; run docker ps to verify
$ docker stop container_id
$ docker start -i container_id
	# start the container in interactive mode.
	# The first command that was used when creating the container will run when you start it again.
	# For an example if container was created using 'docker run -i -t ubuntu:16.10 bash' command,
	# bash will run as the first command.
```

### Nginx and port sharing

```bash
$ docker run -it -p 89:80 ubuntu:16.10 bash
	# -p => share port. Here we are mapping local port 89 to container's port 80
c$ apt-get update && apt-get install -y nginx
	# c$ => from container's shell; just my convention
c$ nginx
	# start nginx
	
# Now from a local terminal (without closing container), try accessing localhost on port 89:
$ curl localhost:89
	# should see standard nginx landing page
```

### Sharing volumes
```bash
$ mkdir ~/dockertest
$ cd ~/dockertest
$ echo 'hello, docker!' > index.html
$ docker run -it -p 89:80 -v ~/dockertest:/var/www/html ubuntu:16.10 bash
	# -v => share volume. Here we are sharing everything inside local machine's ~/dockertest to container's /var/www/html
c$ apt-get update && apt-get install -y nginx
c$ nginx

# Now from a local terminal (without closing container), try accessing localhost on port 89:
$ curl localhost:89
	# You should see our custom page instead of standard nginx landing page
```

That's it for the basics!