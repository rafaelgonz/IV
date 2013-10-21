##EJERCICIO 1
###Crear un espacio de nombres y montar en él una imagen ISO de un CD de forma que no se pueda leer más que desde él. Pista: en ServerFault nos explican como hacerlo, usando el dispositivo loopback

Creamos el espacio de nombre:
    
    sudo unshare -m /bin/bash
    
Y montamos la ISO de la siguiente forma:

mount -o loop CentOS-6.3-i386-LiveCD.iso /mnt




##EJERCICIO 2

###1.Mostrar los puentes configurados en el sistema operativo.
###2.Crear un interfaz virtual y asignarlo al interfaz de la tarjeta wifi, si se tiene, o del fijo, si no se tiene.


Instalamos el paquete:

sudo apt-get install bridge-utils

Y miramos:

![captura 1 ] (https://dl.dropbox.com/s/p96z3ea429xzz3a/cap1.png)

2. Para crear una interfaz virtual:
