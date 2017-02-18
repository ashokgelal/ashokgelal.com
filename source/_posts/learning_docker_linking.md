---
title: Learning Docker - Linking Containers
date: 2017-02-17 21:50:15
tags:
- docker
- sysadmin
- virtualization
---

## Using --link

We can link different containers so that they can talk to each other such as linking nginx and php containers so that we could host dynamic php web apps.

<!--more-->

```bash
$ docker run -d --name=myphp -v $(pwd)/application:/var/www/html ashokgelal/php:0.1.0
# Spin up a php container named "myphp"
```

```bash
$ docker run -d --link=myphp:php -p 80:80 -v $(pwd)/application:/var/www/html ashokgelal/nginx:0.2.0
# Spin up nginx by linking "myphp" container as "php" so the hostname "php" resolves to the IP address of the "myphp" container that we created above
```

## Using Networking

* See available commands:

```bash
$ docker network -h
```

* Create a new network

```bash
$ docker network create --driver=bridge dev-net
# bridge is a default driver and 'dev-net' is the name of the network
```

* Create a Redis container inside dev-net network and name it 'redis'

```bash
$ docker run -d --name=redis --network=dev-net redis:alpine
```

* Create a MySql container inside dev-net network and name it 'mysql'

```bash
$ docker run -d --name=mysql \
    --network=dev-net \
    -e MYSQL_ROOT_PASSWORD=root \
    -e MYSQL_DATABASE=my-app \
    -e MYSQL_USER=app-user \
    -e MYSQL_PASSWORD=app-pass \
    mysql:5.7
```

* Create a PHP container inside dev-net network and name it 'php'

```bash
$ docker run -d --name=php \
    --network=dev-net \
    -v $(pwd)/application:/var/www/html \
    ashokgelal/php:0.1.0
```

* Create a Nginx container inside dev-net network and name it 'nginx'

```bash
$ docker run -d  --name=nginx \
    --network=dev-net \
    -p 89:80 \
    -v $(pwd)/application:/var/www/html \
    ashokgelal/nginx:0.2.0
```

Because all the containers belong to a `dev-net` network, they can talk to each other. One container can belong to multiple containers.

* Inspect the network to see its member containers:

```bash
$ docker network inspect dev-net | jq
```