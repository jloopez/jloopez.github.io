---
layout: post
title:  "LAMP DOCKER-COMPOSE"
date:   2021-11-09 00:00:00 +0300
img: docker.jpg
tags: [sistemas, redes, docker, docker-compose]
---
# Instalación LAMP separando los servicios en 2 máquinas.

Vamos a utilizar 2 máquinas virtuales, en una vamos a instalar un mysqlserver y phpmyadmin con docker-compose y en la otra máquina instalaremos un apache con docker-compose.

## Archivo "docker-compose.yml" en la máquina mysqlserver:

```code
version: '3'
services:
  db:
    images: mysql
    ports:
      - 3306:3306
    command: --default-authentication-plugin=mysql_nativa_password
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
  phpmyadmin:
    image: phpmyadmin
    ports:
      - 8080:80
    environment:
      - PMA_ARBRITRARY=1
```

![docker](img/mysql.png)

## Proyecto en apache:

Vamos a descargar un proyecto web con el que vamos a trabajar. En mi caso voy a utilizar una aplicación de citas medicas publicado en github. El comando que voy a utilizar para descargar es git, quedando de la siguiente manera:

```code
$ sudo git clone https://github.com/sciscar/bookmedik
```
Con esto descargado vamos a hacer la configuración de docker-compose y dockerfile en apache.

## Archivo "docker-compose.yml" en la máquina apache:

```code
version: '3'
services:
  apache:
    build: .
    ports:
      - 8081:80
    restart: always
```

## Archivo "dockerfile" en la máquina apache:

```code
FROM php:7.3-apache
RUN docker-php-ext-install mysqli
COPY ./bookmedik /var/www/html
```

![docker](img/apache.png)

Después editar el archivo "bookmedik/core/controller/Database.php" y cambiar los siguientes campos:

```code
  $this->user="root";
  $this->pass="root";
  $this->host="ipmysqlserver:puerto";
  $this->ddbb="bookmedik";
```

![database](img/databasephp.png)

Y por último ejecutamos lo siguiente en consola para cargar la base de datos de bookmedik en en el servidor de mysql:

```code
$ sudo mysql -u root -h ip-mysql -p < bookmedik/schema.sql
```

Ahora levantamos en ambas máquinas docker-compose y podremos acceder a phpmyadmin en el puerto 8080 y la web en el puerto 8081.

Comandos útiles para docker y docker-compose:

Parar y eliminar todos los contenerdores: $ sudo docker rm $(sudo docker ps -a -q)
Parar todos los contenedores activos: $ sudo docker stop $(sudo docker ps -a -q)
Eliminar todas las imagenes que tenemos en la máquina: $ sudo docker rmi $(sudo docker images -q)


