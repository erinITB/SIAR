<h1 align="center">Instalación del Servidor OCS Inventory NG en Ubuntu</h1>

Primero de todo instalaremos paquetes necesarios para la instalación:
```
sudo apt -y install libxml-simple-perl libdbi-perl libdbd-mysql-perl libapache-dbi-perl libnet-ip-perl libsoap-lite-perl libarchive-zip-perl make build-essential libio-compress-perl 
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

Una vez tenemos el entorno preparado, nos dirijimos a la ruta donde descargaremos OCS:
```
cd /opt
```
Y descargamos el archivo de la <a href="https://ocsinventory-ng.org/?page_id=1548&lang=en">página oficial</a>. En la página oficial te pedirán el correo electrónico y te enviarán los enlaces de descarga a la cuenta que indiques:
```
sudo wget https://github.com/OCSInventory-NG/OCSInventory-ocsreports/releases/download/2.12.1/OCSNG_UNIX_SERVER-2.12.1.tar.gz
```
Una vez descargado, descomprimimos el archivo y nos movemos a la carpeta descomprimida:
```
tar -xzvf OCSNG_UNIX_SERVER-2.12.1.tar.gz
cd OCSNG_UNIX_SERVER-2.12.1
```
Ahora procederemos a la instalación:
```
./setup.sh
```
Durante la instalación nos harán una serie de preguntas para la configuración que responderemos de la siguiente manera:
```
Do you wish to continue ([y]/n)? y

Which host is running database server [localhost] ? ENTER

On which port is running database server [3306] ? ENTER

Where is Apache daemon binary [/usr/sbin/apache2ctl] ? ENTER

Where is Apache main configuration file [/etc/apache2/apache2.conf] ? ENTER

Which user account is running Apache web server [www-data] ? ENTER

Which user group is running Apache web server [www-data] ? ENTER

Where is Apache Include configuration directory [/etc/apache2/conf-available] ? ENTER

Where is PERL interpreter binary [/usr/bin/perl] ? ENTER

Do you wish to setup Communication server on this computer ([y]/n)? y

Where to put Communication server log directory [/var/log/ocsinventory-server] ? ENTER

Where to put Communication server plugins configuration files [/etc/ocsinventory-server/plugins] ? ENTER

Where to put Communication server plugins Perl modules files [/etc/ocsinventory-server/perl] ? ENTER

Do you wish to setup Rest API server on this computer ([y]/n)? y

Where do you want the API code to be store [/usr/local/share/perl/5.x.x] ? ENTER

Do you allow Setup renaming Communication Server Apache configuration file to 'z-ocsinventory-server.conf' ([y]/n) ? y

Do you wish to setup Administration Server (Web Administration Console) on this computer ([y]/n)? y

Where to copy Administration Server static files for PHP Web Console [/usr/share/ocsinventory-reports] ? ENTER

Where to create writable/cache directories for deployment packages, administration console logs, IPDiscover and SNMP [/var/lib/ocsinventory-reports] ? ENTER
------------------------------------------
DON'T FORGET TO RESTART APACHE DAEMON !

Enjoy OCS Inventory NG
```
Una vez instalado habilitaremos las configuraciones de apache:
```
sudo a2enconf ocsinventory-reports.conf 
sudo a2enconf z-ocsinventory-server.conf 
sudo a2enconf zz-ocsinventory-restapi.conf 
```
<b>En estos ficheros tendremos que asegurarnos de que la base de datos, el usuario y la contraseña corresponde con los que hemos creado</b>

Cambiamos los permisos de la carpeta siguiente:
```
sudo chown -R www-data: /var/lib/ocsinventory-reports/ 
```
Reiniciamos el servicio de apache:
```
sudo systemctl restart apache2 
```
Y ya podremos acceder desde el navegador:
```
http://ip-servidor/ocsreports
```
Al entrar nos saldrá una página para configurar la conexión con la Base de Datos donde tendremos que rellenar con la siguiente información:

- ```MySQL login:``` usuario de la base de datos (ocs)
- ```MySQL password:``` contraseña del usuario
- ```Name of Database:``` nombre de la base de datos (ocsweb)
- ```MySQL hostname:``` localhost
- ```MySQL Port:``` puerto que hayamos configurado (3306 por defecto)
- ```Enable SSL:``` NO

El resto de opciones las dejamos vacías.
