---
layout: post
title:  "LEMP DOCKER-COMPOSE"
date:   2021-11-09 00:00:00 +0300
img: lempdockercompose.png
tags: [sistemas, redes]
---
¿Qué es LEMP?

LEMP es un acrónimo compuesto por las iniciales de sus cuatro componentes: Linux,Nginx, MySQL y PHP. Estos forman la infraestructura en el servidor, que hace posible la creación y el alojamiento de páginas web dinámicas.

Vamos a montar nuestro entorno LEAMP, Nginx como proxy, Apache como servidor web, utilizando una máquina virtual con Nginx y con docker-compose para el resto de servicios.

Instalación Nginx en la máquina virtual:

Comandos:

```code
$ sudo apt update
$ sudo apt install nginx
```
Revisamos que está el servicio iniciado.

```code
$ sudo systemctl status nginx.service
```
Por defecto, el document root de nginx es /var/www/html y crea un archivo por defecto llamado "index.nginx-debian.html". Podemos simplificarlo cambiando el nombre a index.html.

```code
$ sudo mv /var/www/html/index.nginx-debian.html /var/www/html/index.html
```

Si queremos cambiar el document root tendría que modificar el archivo "default", está situado en /etc/nginx/sites-available. En el interior tenemos que dejar algo parecido a lo siguiente:

```code
server {
        root /var/www/html/web;  <- Esto es el directorio donde está la web que va a servir.
        index index.html; <- Esto es el que va ha interpretar como principal al acceder al nginx desde el navegador.
        }
```

Ahora vamos a crear el docker-compose.yml con apache, para que lo sirva apache y luego modificaremos el Nginx para hacer el proxy.

```code
version: ‘3’
services:
  apache:
    image: php:7.3-apache
    ports:
      - 8080:80
    volumes:
      - /var/www/html/restaurant-website/app:/var/www/html
```
Ahora levantamos el docker-compose, comando:

```code
$ sudo docker-compose up -d
$ sudo systemctl restart/reload nginx.service
```
