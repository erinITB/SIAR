<h1 align="center">Instalación de FOG Server</h1>

Una vez tengamos nuestro entorno preparado procedemos a instalar, entramos es root

```
sudo -i
```
Acto seguido, instalaremos git:
```
apt-get -y install git
```
Cambiamos a directorio:
```
cd /root
```
Después con el comando git clonaremos el repositorio del programa FOG con el link:
```
git clone https://github.com/FOGProject/fogproject.git
```
Vemos que se ha instalado, acto seguido cambiamos a la carpeta donde se ha descargado todo:
```
cd fogproject/
```
Después cambiamos a la carpeta bin y ejecutamos el instalable:
```
cd /bin
./installfog.sh
```
Le damos al modo normal de instalación al número que corresponda a nuestro sistema operativo.

Luego le damos a tipo de instalación normal

Decimos sí queremos que la interfaz por defecto sea la que tenemos ya asignada.

A continuación nos preguntará si queremos utilizar el fog server como router dhcp o si le queremos instalar el servicio dhcp, también nos preguntará por paquetes de idiomas adicionales, le diremos que si.

Una vez hecho esto nos preguntará si queremos que se envíe información sobre nuestro dispositivo versión de sistema operativo, y la versión de fog, en nuestro caso le damos que sí, aunque depende de cada situación.

Después de eso viene la parte importante, nos hará un resumen de todas las opciones que le hemos dado y nos preguntará si queremos proseguir.

Si vemos que está todo bien le damos que sí y proseguirá a hacer la instalación donde instalará automaticamente todos los paquete (incluidos apache2 para la web, PHP, MySQL,MariaDB, etc…)

Una vez hecho (Puede tardar el proceso un rato largo) nos saldrá el siguiente mensaje diciendo que cuando actualicemos o instalemos la base de datos que le demos continuar, también nos pondrá la ip para conectarnos.

Ahora es cuando nos tenemos que ir a nuestra interfaz gráfica en un buscador que también se ha instalado sola. 

Aquí es donde nos dirá que actualicemos la base de datos. Le daremos click y esperaremos.

Se nos quedará la página cargando, y al final nos pondrá una página con error 504. Significa que se ha acabado el tiempo de espera, que en este caso ya se ha instalado todo.

Ahora es cuando volvemos al server de nuevo y le damos enter, ya que como antes hemos mencionado teníamos que presionar Enter cuando la base de datos se hubiera actualizado/instalado:

Después de un rato, si todo es correcto nos saldrá lo siguiente se actualizará el servidor fog y acto seguido nos dará las credenciales que vienen de manera predeterminada, en este caso usuario contraseña [fog/password]

Una vez hecho esto si refrescamos la página nos saldrá la página de login normal.

Y ahora si con el usuario “fog” y contraseña “password” ya podremos entrar y ya estará listo!


