##EJERCICIO 1
###Crear un espacio de nombres y montar en él una imagen ISO de un CD de forma que no se pueda leer más que desde él. Pista: en ServerFault nos explican como hacerlo, usando el dispositivo loopback

Creamos el espacio de nombre:
    
    sudo unshare -m /bin/bash
    
Y montamos la ISO de la siguiente forma:

mount -o loop CentOS-6.3-i386-LiveCD.iso /mnt


*¿Montas directamente en /mnt?"

##EJERCICIO 2

###1.Mostrar los puentes configurados en el sistema operativo.
###2.Crear un interfaz virtual y asignarlo al interfaz de la tarjeta wifi, si se tiene, o del fijo, si no se tiene.


Instalamos el paquete:

sudo apt-get install bridge-utils

Y miramos:

![captura 1 ] (https://dl.dropbox.com/s/p96z3ea429xzz3a/cap1.png)

**Para crear una interfaz virtual:**

Comenzamos con:
         sudo brctl addbr ej2 

Lo asignamos a la tarjeta fija, ya que con la wifi me daba el error, que hay mencionado en una wiki en el repositorio de clase:

         rafael-K55VM Escritorio # sudo brctl addif ej2 eth0 
 
         rafael-K55VM Escritorio # ip addr show 

          1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN 
          link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00 
          inet 127.0.0.1/8 scope host lo 
          inet6 ::1/128 scope host 
          valid_lft forever preferred_lft forever 
          2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast master ej2 state DOWN qlen 1000 
          link/ether 10:bf:48:15:34:1c brd ff:ff:ff:ff:ff:ff 
          3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP qlen 1000 
          link/ether 44:6d:57:63:fa:c4 brd ff:ff:ff:ff:ff:ff 
          inet 172.20.66.64/23 brd 172.20.67.255 scope global wlan0 
          inet6 fe80::466d:57ff:fe63:fac4/64 scope link 
          valid_lft forever preferred_lft forever 
          4: ej2: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN 
          link/ether 10:bf:48:15:34:1c brd ff:ff:ff:ff:ff:ff 

