<h1 align="center">Instalación del Servidor OCS Inventory NG en Ubuntu</h1>

Primero de todo instalaremos paquetes necesarios para la instalación:
```
sudo apt -y install libxml-simple-perl libdbi-perl libdbd-mysql-perl libapache-dbi-perl libnet-ip-perl libsoap-lite-perl libarchive-zip-perl make build-essential libio-compress-perl nano 
```
Una vez instalados los paquetes anteriores instalaremos varios módulos de PERL:
```
cpan install XML::Entities 
```
Durante la instalación de este módulo nos hará la siguiente pregunta: 

```Would you like to configure as much as possible automatically? [yes]```

Le damos ENTER para continuar y continuamos instalando el resto de módulos:
```
perl -MCPAN -e 'install Mojolicious' 
perl -MCPAN -e 'install Switch' 
perl -MCPAN -e 'install Plack::Handler' 
```
Instalamos apache (en nuestro caso ya lo tenemos instalado por el GLPI) junto a varios módulos necesarios para el funcionamiento de OCS:
```
sudo apt-get install apache2 libarchive-zip-perl libapache2-mod-perl2 libxml-simple-perl libcompress-zlib-perl libdbi-perl libdbd-mysql-perl libapache-dbi-perl libnet-ip-perl libsoap-lite-perl libio-compress-perl libapache-session-perl libapache-rpc-perl libxml-simple-perl libxml-simple-perl libio-compress-perl libnet-ip-perl libwww-perl libcrypt-ssleay-perl libdigest-md5-perl libmojolicious-perl
```
Ahora instalaremos php:
```
sudo apt install php8.x -y
```
Y el resto de librerías de php:
```
sudo apt install php8.x-mysql php8.x-zip php8.x-gd php8.x-mbstring php8.x-curl php8.x-xml php8.x-soap -y 
```
Una vez todo instalado nos aseguramos de que el módulo de Perl esté activado:
```
sudo a2enmod perl 
```
Y editaremos los siguientes ficheros de configuración:
```
sudo nano /etc/php/8.x/apache2/php.ini
sudo nano /etc/php/8.x/cli/php.ini
```
Buscamos en ambos ficheros los siguientes parámetros y los dejamos de esta manera:
```
short_open_tag = On 
post_max_size = 1024M 
upload_max_filesize = 256M
```
Ahora llegaría el momento de instalar la base de datos. En nuestro caso utilizaremos MariaDB que ya hemos instalado y configurado en la <a href="https://github.com/erinITB/SIAR/blob/main/GLPI.md">instalación de GLPI</a>.

Una vez instalado el SGBD nos dispondremos a crear una Base de Datos para nuestro OCS:
```
mysql -u root -p 
CREATE DATABASE ocsweb; 
```
Ahora crearemos un usuario y le daremos permisos para que pueda acceder la Base de Datos:
```
CREATE USER 'ocs'@'localhost' IDENTIFIED BY 'ocs'; 
GRANT ALL PRIVILEGES ON ocsweb.* TO 'ocs'@'localhost' WITH GRANT OPTION; 
FLUSH PRIVILEGES; 
QUIT 
```
<b>Es muy recomendable mantener los nombres ya que son los predeterminados que aparecen en los archivos de configuración de OCS</b>






