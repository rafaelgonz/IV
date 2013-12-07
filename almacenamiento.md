##Ejercicios1
###¿Cómo tienes instalado tu disco duro? ¿Usas particiones? ¿Volúmenes lógicos?

Mi disco duro, después de que windows no me dejara instalar linux, y acudir acertadamente a la oficina de  OSL de Granada, quedó de la siguiente forma:

![pantallazo1](https://dl.dropbox.com/s/80ja6wbaf55f7z4/pantallazo1.png)

Cuyo proceso de instalación, nos lo relataba [Manu Cogolludo](https://twitter.com/Makova65) en el siguiente enlace:

[Instalación linux en portatil Asus k55v](http://osl.ugr.es/2013/10/19/instalar-distro-gnulinux-en-un-asus-modelo-k55v/)


###Si tienes acceso en tu escuela o facultad a un ordenador común para las prácticas, ¿qué almacenamiento físico utiliza?

Los ordenadores de la ETSIIT, utilizan 

###Buscar ofertas SAN comerciales y comparar su precio con ofertas locales (en el propio ordenador) equivalentes.


##Ejercicio2
###Usar FUSE para acceder a recursos remotos como si fueran ficheros locales. Por ejemplo, sshfs para acceder a ficheros de una máquina virtual invitada o de la invitada al anfitrión.


Lo primero que hacemos es instalar sshfs tanto en la jaula, como en el sistema anfitrión, mediante:

    sudo a pt-get install sshfs

Después, asignamos a la jaula la IP 16.8.9.2 a la jaula mediante LXC pannel.

Y llegados a este punto, en la jaula:

    sudo apt-get install sshfs

Y en el equipo anfitrion:

    sudo sshfs ubuntu@16.8.9.2:/home ~/prueba

Y podemos ver los resultados, en dispositivos -> prueba


##Ejercicio3
###Crear imágenes con estos formatos (y otros que se encuentren tales como VMDK) y manipularlas a base de montarlas o con cualquier otra utilidad que se encuentre

He creado una imagen con raw, cuyo formato evita los espacios sin asignar, que se representan por metadatos y por lo tanto puede usar en el almacenamiento físico menos espacio del asignado inicialmente. Lo admiten la mayoría de los sistemas operativos modernos.

Para crearlo realizamos lo del siguiente pantallazo, así como la orden para ver los bloques disponibles, para lo que tenemos dos opciones:

    ls -lks fichero-suelto.img 
    fallocate -l 5M fichero-suelto.img

Pero este último, no funciona, tal y como dice el guión de prácticas, que podría pasar en algunos sistemas operativos.

![pantallazo2](https://dl.dropbox.com/s/8jnjsnpq2kf0e4n/pantallazo2.png)
