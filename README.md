# Wordpress Docker-compose

Install un nouveau wordpress avec proxy Traefik / Mariadb database


Table of Contents
-----------------

#### Introduction

- [Prerequisites](#prerequisites)

#### The application

- [The architecture](#the-architecture)
- [The important files are](#the-important-files-are)
- [The docker-compose](#running-the-postgresql-database)
- [Update the network config](#the-crontab)
- [Deployment](#deployment)
- [Logs stream](#logs-stream)

Prerequisites
---------------

### 1. Test localy this project

```
docker-compose up -d
```

For exemple :


The architecture
---------------

### 1. Stack

* [DOCKER](https://www.docker.com/products/docker-desktop) - Container are in use here 
* [WORDPRESS DOCKER](https://hub.docker.com/r/h2g2/docker-xenial) -
* [TRAEFIK DOCKER](https://hub.docker.com/r/h2g2/docker-xenial) -
* [MARIADB DOCKER](https://hub.docker.com/r/h2g2/docker-xenial) -

### 2. Description

Install un nouveau wordpress avec proxy Traefik / Mariadb database


### 3. Fichiers importants :

<bold>Container definition : </bold>

- docker-compose.yml = script to start container

<bold>Environement : </bold>

- .env.dist = 
- .env = 


#### Exemple create a new wordpress (new instance)
---------------

### 1. Create a new wordpress 

Deployment
---------------

Clone the repository on instance
```
cd /home
git clone https://github.com/paulbaudrier/wordpress-bluesoft
```

Simply create the container with :
```
docker-compose up -d
```

See [Logs stream section](#logs-stream) for more info about logs

Logs stream
---------------

### 1. Main Log stream

get container name with :
```
docker ps
```

and you can get the container logs with :
```
docker logs 
```

#### Exemple 2 : Add new wordpress (same instance)
---------------

### 1. Add a new wordpress 

Deployment
---------------

Vim docker-compose.yml
Changer le port / Host traefik
```
### WORDPRESS CONTAINEUR ###
  wordpress_two:
    depends_on:
      - db
      - traefik
    image: wordpress:latest
    ports:
      - "8082:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: $MYSQL_USER
      WORDPRESS_DB_PASSWORD: $MYSQL_PASSWORD
      WORDPRESS_DB_NAME: $MYSQL_DATABASE
    volumes:
      - wordpress:/var/html/www 
    labels:
      - "traefik.enable=true"
      # URL to reach this container
      - "traefik.http.routers.wordpress.rule=Host(`boutique02.macloudcompany.com`)"
      # Activation of TLS
      - "traefik.http.routers.wordpress.tls=true"
```

Simply create the container with :
```
docker-compose up -d
```

See [Logs stream section](#logs-stream) for more info about logs