---
layout: post
title:  "LAMP en Debian/Ubuntu"
date:   2021-09-17
img: FF59B5E9-27DE-439E-84B3-9D0CD39EB6A8.jpeg
tags: [sistemas, Debian, Ubuntu, Apache2, PHP, MySQL]
---

El acrónimo LAMP está compuesto por las iniciales de sus cuatro componentes: Linux, Apache, MySQL y PHP. Estos forman la infraestructura en el servidor, que hace posible la creación y el alojamiento de páginas web dinámicas. Para montar nuestro propio entorno LAMP, primero actualizamos el sistema.

### Actualizar sistema
```code

jloopez:~# apt update -y && apt upgrade -y

```

### Instalación de Apache
```code

jloopez:~# apt install apache2

```
Verificamos que se ha instalado y que el servicio está en marcha.
```code

jloopez:~# systemctl status apache2

```
### Instalación de MySQL
```code

jloopez:~# apt install mysql-common mysql-client mysql-server

```
Durante la instalación del servicio se nos pedirá la contraseña del usuario root del servidor mysql.

### Instalación de PHP
```code

jloopez:~# apt install php libapache2-mod-php php-mysql

```

### Instalación de PHPMyAdmin
Como gestor de la base de datos podemos utilizar phpmyadmin, que es una aplicación php que me permite acceder a todas las funciones de MySQL.
```code

jloopez:~# apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl

```
En la instalación del paquete phpmyadmin nos preguntará el servidor web que estamos utilizando, para realizar la configuración automática. En nuestro caso escogeremos la opción Apache2.

## Prueba de funcionamiento
Para probar el funcionamiento de Apache y PHP es habitual crear un documento info.php en el directorio /var/www/html con el siguiente contenido:
```code
<html>
<body>
   <? echo phpinfo(); ?>
</body> 
</html> 
```

Para acceder desde el navegador del cliente al servidor web vamos a utilizar la IP del servidor seguido de infor.php.

Ejemplo: 192.168.1.22/info.php





---
