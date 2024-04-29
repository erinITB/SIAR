<h1 align="center">Instalación de GLPI</h1>

Lo primero que haremos será instalar apache, que es donde correrá GLPI:
``` 
sudo apt-get install apache2
```
Una vez hemos instalado apache, instalaremos un SGBD que en nuestro caso será mysql:
``` 
sudo apt-get install mysql-server
```
Cambiamos la contraseña a root por la que consideremos:
```
mysql -u root -p 
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
exit
```

También necesitaremos instalar php ya que GLPI trabaja con este:
```
sudo apt install php libapache2-mod-php
```
Ya tenemos lo imprescindible para instalar GLPI. Ahora descargamos la versión de GLPI desde la <a href="https://glpi-project.org/es/descargar-software/">página oficial</a>:
```
wget https://github.com/glpi-project/glpi/releases/download/10.0.x/glpi-10.0.x.tgz
```
La descomprimimos y la movemos al directorio de nuestro servidor web:
```
tar -xzf glpi-10.0.x.tgz
sudo mv glpi/var/www/html
```
Ahora ya podriamos acceder al asistente de instalación pero antes, haremos un par de pasos previos para poder instalarlo.
- Primero de todo cambiaremos los permisos de la carpeta de GLPI:
```
sudo chown -R www-data:www-data /var/www/html/glpi
```
- A continuación instalaremos unas extensiones y dependencias necesarias para la instalación:
```
sudo apt install php8.1-{mysql,xml,curl,gd,intl,ldap,bz2,zip,mbstring} php-cas
```
- Por último crearemos la base de datos sobre la que trabajará GLPI:
```
sudo mysql -u root -p
create database GLPI;
exit
```

Llega el momento de acceder al GLPI mediante el navegador para poder acceder al asistente de instalación. Para acceder pondremos la ip o dominio del servidor/glpi(ej: 192.168.10.10/glpi). 
Una vez estemos dentro le daremos a continuar eligiendo las opciones según nuestras preferencias hasta que lleguemos al primer paso de la configuración:
- Paso 1: SQL server: ```ip o dominio del servidor``` - SQL user: ```root``` - SQL password: ```contraseña de root```

  










