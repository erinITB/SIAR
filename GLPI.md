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
exit;
```

También necesitaremos instalar php ya que GLPI trabaja con este:
```
sudo apt install php libapache2-mod-php
```
Ya tenemos lo imprescindible para instalar GLPI. Ahora descargamos la versión de GLPI desde la <a href="https://glpi-project.org/es/descargar-software/">página oficial</a>:
