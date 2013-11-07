
##Ejercicios 3
###1. Usar debootstrap (o herramienta similar en otra distro) para crear un sistema mínimo que se pueda ejecutar más adelante.

###2. Experimentar con la creación de un sistema Fedora dentro de Debian usando Rinse.

Instalamos debootstrap:

		sudo apt-get install debootstrap

E instalamos la versión quantal, tal y como viene en el ejemplo de la documentación:

		sudo debootstrap --arch=amd64 quantal /home/rafael/UNIVERSIDAD/IV/ http://archive.ubuntu.com/ubuntu/

Y al cabo de unos minutos, ya tienes la instalación de la versión de ubuntu seleccionada.

**2 parte**

Para esto, instalamos rinse, con apt-get install rinse y la síntaxis de rinse para esta instalación sería la siguiente:

                sudo rinse --distribution fedora-19 --arch amd64 --directory IV/


Llegados a este punto, entraríamos en el directorio IV donde se ha instalado, y le damos permisos con:

                chroot IV

Y ya sólo nos quedaría:

                mount -t proc none IV/proc/

                mount -t none /dev IV/dev/ -o bind

Bibliografía:  http://gatocomputin.blogspot.com.es/2013/06/instalar-centos-6-en-un-chroot-en.html


##EJERCICIO 4
###Instalar alguna sistema debianita y configurarlo para su uso. Trabajando desde terminal, probar a ejecutar alguna aplicación o instalar las herramientas necesarias para compilar una y ejecutarla.

Para instalar un sistema Debian, voy a usar debootstrap de la siguiente forma:

             sudo debootstrap --arch=amd64 wheezy /home/Documentos/ http://ftp.debian.org/debian/

Y para ejecutar/instalar aplicaciones hemos realizado lo siguiente:

Nos metemos en chroot:

![captura 1 ] (https://dl.dropbox.com/s/p55ycry4g5zfyav/pantallazo1.png)

y montamos lo siguiente:

      mount -t proc proc /proc

Y probamos a ejecutar top

![captura 2 ] (https://dl.dropbox.com/s/x4gg97p4hp2s4ft/pantallazo2.png)

