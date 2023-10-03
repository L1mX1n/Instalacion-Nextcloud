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

```console
[alumne@elpuig example]$ vagrant init ubuntu/jammy64
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
[alumne@elpuig example]$ ll
total 4
-rw-rw-r--. 1 alumne alumne 3020 15 jul. 14:23 Vagrantfile
[alumne@elpuig example]$
```

Ara podem aixecar tota la infraestructura (afegint el paràmetre `--provider=virtualbox` perquè en algunes màquines el provider per defecte és `libvirt`) amb `vagrant up`:

```console
[alumne@elpuig example]$ vagrant up --provider=virtualbox
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default: 
    default: Guest Additions Version: 6.0.0 r127566
    default: VirtualBox Version: 6.1
==> default: Mounting shared folders...
    default: /vagrant => /home/alumne/example

[alumne@elpuig example]$
```

Aquesta comanda descàrrega (les màquines descarregades es guarden a `~/.vagrant.d/`) —si cal— la màquina utilitzada, crea una MV a `VirtualBox`, la configura, l'encén i la prepara amb la clau pública del host per poder iniciar sessió amb `ssh`.

```console
[alumne@elpuig example]$ vagrant ssh
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-77-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu Jul 15 12:38:47 UTC 2021

  System load:  0.0               Processes:               110
  Usage of /:   3.2% of 38.71GB   Users logged in:         0
  Memory usage: 19%               IPv4 address for enp0s3: 10.0.2.15
  Swap usage:   0%


1 update can be applied immediately.
To see these additional updates run: apt list --upgradable


vagrant@ubuntu-jammy:~$
```

A més, per defecte s'ha compartit el directori del projecte (`~/example`) entre la màquina física i la màquina virtual. Així resulta molt senzill compartir fitxers ja que el directori del projecte estarà muntat a la MV al directori `/vagrant`:

```console
vagrant@ubuntu-jammy:~$ ll /vagrant
total 8
drwxrwxr-x  1 vagrant vagrant   38 Jul 15 12:32 ./
drwxr-xr-x 20 root    root    4096 Jul 15 12:33 ../
drwxrwxr-x  1 vagrant vagrant   32 Jul 15 12:32 .vagrant/
-rw-rw-r--  1 vagrant vagrant 3020 Jul 15 12:23 Vagrantfile
vagrant@ubuntu-jammy:~$
```

La comanda `vagrant status` ens mostrarà informació sobre l'estat de les nostres MVs i les podrem aturar amb `vagrant halt` o suspendre amb `vagrant suspend`. En qualsevol cas, es podran tornar a encendre amb `vagrant up`.

Quan ja no siguin necessàries les MVs es podran esborrar amb `vagrant destroy`.