---
title: Learning Docker - Everyday Use
date: 2017-02-17 11:54:15
tags:
- docker
- sysadmin
- virtualization
---

With Docker, not only you can spin-off your own containers from a base image, but you can create your own image with some custom libraries installed. It sort of works like git.

* After installing nginx, diff your container:

```bash
$ docker diff container_id
# see differences
```

* Commit the changes

```bash
$ docker commit -a "Ashok Gelal" -m "Install nginx" container_name ashokgelal/nginx:0.1.0
# After this, a new image ashokgelal/nginx will be available as a base image
$ docker images
```

* Run nginx from our own base image

```bash
$ docker run -it -p 89:80 -v $(pwd):/var/www/html ashokgelal/nginx:0.1.0 nginx
```

The above method runs nginx but because it is running as a daemon, Docker kills the container thinking there is nothing running. To avoid that, one thing we can do is to make nginx not run as a daemon:

```bash
$ docker run -it -p 89:80 -v $(pwd):/var/www/html ashokgelal/nginx:0.1.0 nginx
c$ echo 'daemon off;' >> /etc/nginx/nginx.conf
c$ exit
$ docker commit -a "Ashok Gelal" -m "Nginx runs in a non-daemon mode" container_id ashokgelal/nginx:0.2.0
# create a new image with the latest changes

$ docker run -it -p 89:80 -v $(pwd):/var/www/html ashokgelal/nginx:0.1.0 nginx
```

Just like git, we can check the history of an image as well:
```bash
$ docker history ashokgelal/nginx:0.1.0
```

