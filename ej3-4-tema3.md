##Ejercicio 3

###Crear y ejecutar un contenedor basado en Debian.


En este apartado, he optado por la instalación de ubuntu:
    
    sudo lxc-create -t ubuntu -n una-caja
    
    
Y para entrar a ella, tal y como hemos hecho hasta ahora en este tema:
    
    sudo lxc-start -n una-caja


Donde:

    usuario: ubuntu / password: ubuntu

![pantallazo2](https://dl.dropbox.com/s/ywr4z2r4epe47bx/pantallazo2.jpg)



###Crear y ejecutar un contenedor basado en otra distribución, tal como Fedora.
###Nota En general, crear un contenedor basado en tu distribución y otro basado en otra que no sea la tuya.


He creado una jaula Centos, siguiendo el siguiente tutorial:

http://www.bonusbits.com/main/HowTo:Setup_CentOS_LXC_Container_on_Ubuntu

He instalado lo siguiente:

    sudo apt-get install librpm3 librpmbuild3 librpmio3 librpmsign1 libsqlite0 python-rpm python-sqlite python-sqlitecachec python-support python-urlgrabber rpm rpm-common rpm2cpio yum debootstrap bridge-utils

Y seguidamente me he descardado el template: https://gist.github.com/hagix9/3514296#file-lxc-centos


Al descargarse, realizamos finalmente lo siguiente:

    sudo cp ~/Downloads/lxc-centos /usr/share/lxc/templates/

    sudo chmod +x /usr/share/lxc/templates/lxc-centos
    
Creamos la jaula:

    lxc-create -n lxc-centos01 -t centos

![pantallazo7](https://dl.dropbox.com/s/zld9n1vkl9m9dix/pantallazo7.jpg)


Y una vez instalada la jaula, arrancamos la jaula y nos identificamos, con password "password"

    lxc-start -n lxc-centos01
    

![pantallazo8](https://dl.dropbox.com/s/f9x6qm1g24wbeab/pantallazo8.jpg)


##Ejercicio 4 

###Instalar lxc-webpanel y usarlo para arrancar, parar y visualizar las máquinas virtuales que se tengan instaladas.

Para instalarlo, lo descargamos desde la página web, y realizamos lo siguiente:

![pantallazo4](https://dl.dropbox.com/s/h2w9gmfxsomfw5j/pantallazo4.jpg)

Y una vez descargado e instalado, comprobamos que funciona:

![panallazo5](https://dl.dropbox.com/s/j7docntnz1fc3nv/pantallazo5a.jpg)

admin / admin

![pantallazo6](https://dl.dropbox.com/s/9qezvik2ox7xijh/pantallazo5.jpg)


###Desde el panel restringir los recursos que pueden usar: CPU shares, CPUs que se pueden usar (en sistemas multinúcleo) o cantidad de memoria.


Para realizar este apartado, navegamos por el panel, y como observamos en la siguiente captura, podemos modificar prácticamente todo, nombre, número de núcleos, ip...

![pantallazo7](https://dl.dropbox.com/s/ix3tbepn2ncc5yt/pantallazo6.png)
