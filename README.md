# Instalacion-Vagrant
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
vagrant up --provider=virtualbox
```
Una vez montado ya podremos usar `ssh`, para entrar a la MV que ha montado el comando anterior.
```console
smx2b@turing-116:~$ vagrant ssh
smx2b@turing-116:~$ ll /vagrant
```
### Otros comandos:
`vagrant status`: Nos muestra informacion sobre el estado de las MVs.
`vagrant halt`: Parar las MVs
`vagrant suspend`: Suspender las MVs
`vagrant up`: Encender las MVs
`vagrant destroy`: Borrar las MVs