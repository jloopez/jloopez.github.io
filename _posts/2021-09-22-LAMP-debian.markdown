---
layout: post
title:  "LAMP en Debian/Ubuntu"
date:   2021-09-22 00:00:00 +0300
img: FF59B5E9-27DE-439E-84B3-9D0CD39EB6A8.jpeg
tags: [sistemas, Debian, Ubuntu, Apache2, PHP, MySQL]
---
¿Qué es LAMP?

LAMP es un acrónimo compuesto por las iniciales de sus cuatro componentes: Linux, Apache, MySQL y PHP. Estos forman la infraestructura en el servidor, que hace posible la creación y el alojamiento de páginas web dinámicas.

Vamos a montar nuestro entorno LAMP en una máquina virtual que ya tenemos instalada con Debian o deviradas.

### Paso 1. Actualizar sistema
```code

jloopez:~# sudo apt update -y && apt upgrade -y

```

### Paso 2. Instalación de Apache
```code

jloopez:~# sudo apt install apache2

```
Verificamos que se ha instalado y que el servicio está en marcha.
```code

jloopez:~# sudo systemctl status apache2

```
### Paso 3. Instalación de MySQL
```code

jloopez:~# sudo apt install mysql-common mysql-client mysql-server

```
Durante la instalación del servicio se nos pedirá la contraseña del usuario que crea por defecto como root para el servidor mysql.

### Paso 4. Instalación de PHP
```code

jloopez:~# sudo apt install php libapache2-mod-php php-mysql

```
