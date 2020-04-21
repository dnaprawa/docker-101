# Docker Workshop for beginners

This repo contains a list of commands used on workshop "Docker Od Podstaw". It includes also sample application we can build and run by own. 


## Exercise 1

Running first containers:

```sh
docker container run hello-world
docker container run ubuntu:latest
docker container run ubuntu:latest ls -l

docker container run -it ubuntu bash
docker container run -it -d ubuntu bash
docker container ls
docker container exec -it <container_id> bash
```


## Exercise 2

Running services:

### NGINX
```sh
docker pull nginx
docker container run -d -p 80:80 --name mynginx nginx
```

### Postgres

```sh
docker pull postgres
docker run -d -e POSTGRES_USER=<USER_HERE> \
-e POSTGRES_PASSWORD=<PASSWORD_HERE> -p 5444:5432 postgres
```

## Exercise 3

Modifying container files:

```sh
docker container exec -it mynginx bash
apt-get update && apt-get install -y nano
nano /usr/share/nginx/html/index.html
docker commit mynginx mynginx:v1
```

## Exercise 4

Building own image:

```sh
cd first_app_in_docker
docker image build . -t myapp:1.0
```

Pushing to Docker Hub

```sh
docker image push <username>/<repository_name>:<tag>
```

## Exercise 5

Running WordPress using commands:

```sh
docker network create -d bridge wp

docker run -d -p 3306:3306 --name db -e MYSQL_DATABASE=exampledb \
-e MYSQL_USER=exampleuser -e MYSQL_PASSWORD=examplepass \ 
-e MYSQL_RANDOM_ROOT_PASSWORD=1 --network=wp \
--restart=always mysql:5.7 

docker run -d -p 8080:80 -e WORDPRESS_DB_HOST=db:3306 \
-e WORDPRESS_DB_USER=exampleuser -e WORDPRESS_DB_PASSWORD=examplepass \
-e WORDPRESS_DB_NAME=exampledb --network=wp \
--restart=always wordpress:latest
```

## Exercise 6

Running WordPress using docker-compose:

```sh
cd wordpress
docker-compose up -d
docker-compose down
```

To delete volumes data use following command:
```sh
docker-compose down -v
```