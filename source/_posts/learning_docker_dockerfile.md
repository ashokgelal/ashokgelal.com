---
title: Learning Docker - Dockerfile
date: 2017-02-17 11:54:15
tags:
- docker
- sysadmin
- virtualization
---

Sysadmin job is no fun unless you can automate boring and repetitive tasks. All the commands we have learned so far could be automated by putting all the commands in a `Dockerfile` and we can use `docker build` command to automatically build a container.

* Create a Dockerfile:
```bash
$ mkdir nginx
cd nginx
vim Dockerfile
```

* Populate Dockerfile:

```bash
FROM ubuntu:16.10
MAINTAINER Ashok Gelal

RUN apt-get update && apt-get install -y nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

CMD ["nginx"]
```

* Build a container from a Dockerfile:

```bash
docker build -t ashokgelal/nginx:0.1.0 .
```

```bash
docker build -f ./Dockerfile -t ashokgelal/nginx:0.1.0 ./build
# This just builds a new image, names it and tags as 0.1.0
# build => build from a Dockerfile
# -f ./Dockerfile => set the Dockerfile if it is named other than Dockerfile
# -t => tag the resulting image. We can use -t flag multiple times
# ./build => This is the "context directory"
```





Every command/ directive we put in the Dockerfile adds a new layer into the container adding extra space and cruft. So, it's important to add as much data as we can into each directive, such as `RUN`.

