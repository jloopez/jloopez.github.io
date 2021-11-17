---
layout: post
title:  "LAMP BALANCEO DOCKER-COMPOSE"
date:   2021-11-09 00:00:00 +0300
img: haproxy.png
tags: [sistemas, redes, docker, docker-compose, apache, balanceo]
---

# Instalación LAMP con docker compose, utilizando un proxy con balanceo de carga.

El docker compose va a estar compuesto por:

- 1 Mysql
- 1 PhpMyAdmin
- 1 Build -> dockerfile -> php:7.3-apache
- 1 Proxy apache

El documento docker-compose.yml quedaría así:

```code
version: '3.1'

services:
  db:
    image: mysql
    volumes:
      - datos_db:/var/lib/mysql
      - ./bookmedik:/docker-entrypoint-initdb.d
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: toor
  phpmyadmin:
    image: phpmyadmin
    restart: always
    ports:
      - 8080:80
    environment:
      - PMA_ARBRITARY=1
  apache:
    build: .
    volumes:
      - ./bookmedik:/var/www/html
  balanceo:
    image: dockercloud/haproxy
    ports:
      - 80:80
    links:
      - apache
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
volumes:
   datos_db:
```

![compose-balanceo](https://github.com/jloopez/jloopez.github.io/blob/master/assets/img/compose-balanceo.png?raw=true)

El documento dockerfile quedaría así:

```code

FROM php:7.3-apache
RUN docker-php-ext-install mysqli

```
![dockerfile-balanceo](https://github.com/jloopez/jloopez.github.io/blob/master/assets/img/dockerfile-balanceo.png?raw=true)


Ahora la diferencia está al ejecutar el dockercompose, que tenemos que añadir la opción "--escale apache=4". 
Esto hace que el contenedor "web" definido en el docker-compose, levante el número que le especificamos.
En mi caso crearía 4 apaches, en los que el proxy se encargara del balanceo de carga.

```code

$ sudo docker-compose up -d --escale apache=4

```
