# Instalacion-Nextcloud
## Vagrant
Para instalar Nextcloud tendremos que usar `Vagrant`, creamos un directorio con cualquier nombre. Toda la configuracion del proyecto se escrirá en el fichero `Vagrantfile`.
```console
smx2b@turing-116:~$ mkdir Ejemplo
smx2b@turing-116:~$ cd Ejemplo
```

Podemos crear directamente el fichero `Vagrantfile` con el siguiente comando: `vagrant init <box>`.
```console
smx2b@turing-116:~$ vagrant init ubuntu/jammy64
smx2b@turing-116:~$ ll
```

Una vez creado, levantamos la infraestructura con el siguiente comando y parametro: `vagrant up` `--provider=virtualbox`.
```console
smx2b@turing-116:~$ vagrant up --provider=virtualbox
```
Una vez montado ya podremos usar `ssh`, para entrar a la MV que ha montado el comando anterior.
```console
smx2b@turing-116:~$ vagrant ssh
smx2b@turing-116:~$ ll /vagrant
```
### Otros comandos:
- `vagrant status`: Nos muestra informacion sobre el estado de las MVs.
- `vagrant halt`: Parar las MVs
- `vagrant suspend`: Suspender las MVs
- `vagrant up`: Encender las MVs
- `vagrant destroy`: Borrar las MVs

## Instalacion y configuracion de aplicaciones web
Para instalar una aplicacion web, necesitamos su codigo fuente y traerlo al directorio de nuestro servidor de aplicaciones, en este caso apache2. Cuanto instalas apache2 se crea una carpeta en `/var/www/html`. Si llevamos nuestra aplicacion al directorio `/var/www/html` tendremos acceso a nuestra aplicacion con la direccion `http://localhost`.

### Instalacion Apache2, Mysql, librerias
- Dentro de la MV, actualizaremos la maquina con los comandos: `apt update` y `apt upgrade`.
```console
smx2b@turing-116:~$ apt update
smx2b@turing-116:~$ apt upgrade
```
1. Instalacion `apache2`.
```console
apt install -y apache2
```
2. Instalacion del servidor de bases de datos `mysql-server`.
```console
apt install -y mysql-server
```
3. Instalacion de librerias `php` (Lenguaje principal que usan las aplciaciones).
```console
apt install -y php libapache2-mod-php
apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```
4. Reinicio servidor apache2
```console
systemctl restart apache2
```
**RECORDAR SER ROOT**

### Configuracion MySQL
#### Accedemos a la consola de MySQL
Desde una terminal ejecutamos el comando siendo `root`.
```console
mysql
```

