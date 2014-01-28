##Ejercicios1
###¿Cómo tienes instalado tu disco duro? ¿Usas particiones? ¿Volúmenes lógicos?

Mi disco duro, después de que windows no me dejara instalar linux, y acudir acertadamente a la oficina de  OSL de Granada, quedó de la siguiente forma:

![pantallazo1](https://dl.dropbox.com/s/80ja6wbaf55f7z4/pantallazo1.png)

Cuyo proceso de instalación, nos lo relataba [Manu Cogolludo](https://twitter.com/Makova65) en el siguiente enlace:

[Instalación linux en portatil Asus k55v](http://osl.ugr.es/2013/10/19/instalar-distro-gnulinux-en-un-asus-modelo-k55v/)



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

Para crearlo realizamos dos opciones:
    
    
    fallocate -l 5M fichero-suelto.img
    dd of=fichero-suelto.img bs=1k seek=5242879 count=0

Y para visuarlizarlo:

     ls -lks fichero-suelto.img 

///Fallocate, en un principio creía que servía para visualizarlo, pero sirve para crear imagenes, por lo que en un principio pensé que no servía en linux mint por ese motivo, pero funciona perfectamente.

![pantallazo2](https://dl.dropbox.com/s/8jnjsnpq2kf0e4n/pantallazo2.png)


Otra imagen, creada y manupulada, la hemos realizado con  qcow2 que es un formato usado inicialmente por QEMU pero más adelante generalizado a casi todos los gestores de MVs de Linux. Es un sistema que usa copy on write para mantener la coherencia del resultado en memoria con lo que hay en disco a la vez que se optimiza el acceso al mismo.

Instalamos qemu mediante:

         sudo apt-get install qemu-utils

Y creamos la imagen, tal y como vemos en el guión de prácticas:

        qemu-img create -f qcow2 fichero-cow.qcow2 5M


![pantallazo3](https://dl.dropbox.com/s/0a66otk63ycqj2n/pantallazo3.png)


Para ver estas imagenes, podríamos montarlas con:

        mount -o loop,offset=32256 /camino/a/fichero-suelto.img
        /mnt/mountpoint

Y:

        modprobe nbd max_part=16
        qemu-nbd -c /dev/nbd0 fichero-cow.qcow2
        partprobe /dev/nbd0
        mount /dev/nbd0p1 /mnt/image
        
##Ejercicio4
###Crear uno o varios sistema de ficheros en bucle usando un formato que no sea habitual (xfs o btrfs) y comparar las prestaciones de entrada/salida entre sí y entre ellos y el sistema de ficheros en el que se encuentra, para comprobar el overhead que se añade mediante este sistema

Lo primero que vamos a realizar, es crear las imagenes con qemu, tal y como hicimos en el ejercicio anterior, con xfs:

	qemu-img create -f raw xfs.img 5M
	
Y lo convertimos en sistema de ficheros en bucle:

	sudo losetup -v -f xfs.img
	
Le damos formato:

	sudo mkfs.xfs /dev/loop1
	
Y lo montamos para terminar:

	sudo mount /dev/loop0 /mnt/loop1/

Y lo comprobamos:

![pantallazo4](https://dl.dropbox.com/s/025svayigsqxxza/pantallazo4.png)

	
Comprobamos la gran velocidad, y buen funcionamiento que presentan los ficheros en bucle, al copiar archivos en el.



##Ejercicio5
###Instalar ceph en tu sistema operativo.

Para instalarlo, realizamos:

![pantallazo](https://dl.dropbox.com/s/b433mf5tvhuazst/pantallazo11.png)


##Ejercicio6
###Crear un dispositivo ceph usando BTRFS o XFS

Lo primero que tenemos que hacer es crear los directorios donde se va a almacenar la información de CEPH

    sudo mkdir -p /srv/ceph/{osd,mon,mds}
    
Y creamos un fichero de configuración, en:

    /etc/ceph/ceph.conf:

    [global]
    	log file = /var/log/ceph/$name.log
	pid file = /var/run/ceph/$name.pid
    [mon]
	 mon data = /srv/ceph/mon/$name
    [mon.rafa]
	 host = ubuntu
	 mon addr = 127.0.0.1:6789
    [mds]
    [mds.rafa]
	 host = ubuntu
    [osd]
	 osd data = /srv/ceph/osd/$name
	 osd journal = /srv/ceph/osd/$name/journal
	 osd journal size = 1000
    [osd.0]
	 host = ubuntu
	 xfs devs = /dev/loop0

 
Creamos un fichero en bucle igual al del ejercicio 4, y realizamos lo siguiente:
    
     qemu-img create -f raw ceph_ej6.img 2G
     sudo losetup -v -f ceph_ej6.img
     sudo mkfs.xfs /dev/loop0
   
Y:

     sudo mkdir /srv/ceph/osd/osd.0
     
Y creamos el sistema de ficheros:

    sudo /sbin/mkcephfs -a -c /etc/ceph/ceph.conf 
    
![pantallazo12](https://dl.dropbox.com/s/yeqfn2mo6znmviy/pantallazo12.png)

Una vez llegados a este punto, iniciamos el servicio:

	sudo /etc/init.d/ceph -a start

Y vemos el status de ceph:

![pantallazo13](https://dl.dropbox.com/s/ihdzvcqw4neahmy/pantallazo13.png)
	
Y finalmente, creamos el directorio, donde vamos a montar el dispositivo:

	sudo mount -t ceph ubuntu:/ /mnt/ceph


##Ejercicio7
###Almacenar objetos y ver la forma de almacenar directorios completos usando ceph y rados.

Para trabajar con rados, lo primero que debemos hacer es crear la piscina:

	sudo rados mkpool ejercicio7

Para comprobar lo que hay, utilizamos:

	sudo rados df

![pantallazo14](https://dl.dropbox.com/s/k4v2qtmaxkcau6d/pantallazo14.png)

Y comprobamos que está vacio, por lo que vamos a introducir una de las imagenes creadas en los ejercicios anteriores mediante:

	sudo rados put -p ejercicio7 objeto ceph_ej6.img

Y lo listamos, para comprobar que se ha creado:

	rados ls -p prueba-piscina
	
	
##Ejercicio8
###Tras crear la cuenta de Azure, instalar las herramientas de línea de órdenes (Command line interface, cli) del mismo y configurarlas con la cuenta Azure correspondiente.

Siguiendo el tutorial presentado en el enunciado, instalamos node.js, añadiendo el repositorio correspondiente:

![pantallazo5](https://dl.dropbox.com/s/82m42priqzhvfn2/pantallazo5.png)

E instalamos:

	sudo apt-get install nodejs
	
Llegados a este punto, tenemos que instalar Windows Azure Cross-Platform Command-Line Interface:
	
	npm install azure-cli

![pantallazo6](https://dl.dropbox.com/s/2d7fordxhx5w9ak/pantallazo6.png)


Una vez instalado, nos vamos a http://go.microsoft.com/fwlink/?LinkId=254432 y hacemos login. Se descargará un archivo, gracias al cuál podemos  seguir con el ejercicio.

Y lo importamos:

	azure account import ~/Azpad245GZK8973-12-30-2013-credentials.publishsettings
	
![pantallazo7](https://dl.dropbox.com/s/j1aknrqvp3bbkfi/pantallazo7.png)


Para comprobar que hemos importado nuestra cuenta, listamos:

	azure account list
	
![pantallazo8](https://dl.dropbox.com/s/n1zwshudsp9evcv/pantallazo8.png)

	
Una vez llegados a este punto, vamos a crear una cuenta de almacenamiento, y para ello:

	azure account storage create rafaelgonz
	azure account storage keys list rafaelgonz
	
	export AZURE_STORAGE_ACCOUNT=rafaelgonz
	export AZURE_STORAGE_ACCESS_KEY=*
	echo $AZURE_STORAGE_ACCOUNT
	echo $AZURE_STORAGE_ACCESS_KEY

*La llave nos la da azure account storage keys list rafaelgonz

![pantallazo9](https://dl.dropbox.com/s/j8nss7rnkkku4ks/pantallazo9.png)



##Ejercicio9
###Crear varios contenedores en la cuenta usando la línea de órdenes para ficheros de diferente tipo y almacenar en ellos las imágenes en las que capturéis las pantallas donde se muestre lo que habéis hecho.

Vamos a crear un contenedor para imágenes:

	azure storage container create imagenes -p blob
	

Y ahora vamos a subir una imágen a dicho contenedor, mediante:

	azure storage blob upload ~/Documentos/Imágenes/banda.jpg
	
![pantallazo10](https://dl.dropbox.com/s/gskg7b0e9tu8jot/pantallazo10.png)

Y con esto, hemos subido archivos a la cuenta realizada en el ejercicio anterior.



##Ejercicio10
###Desde un programa en Ruby o en algún otro lenguaje, listar los blobs que hay en un contenedor, crear un fichero con la lista de los mismos y subirla al propio contenedor. Muy meta todo.

Vamos a realizar el pequeño programa en python, cuyo código es el siguiente:


	import credentials  
	from azure.storage import BlobService
	
	
	def getContainersWithBlobs(blob_service):
	    
	    #CONTENEDORES
	    for i in blob_service.list_containers().containers:
	        print("Contenedores:")
	        print("Nombre: {}".format(i.name))
	        print("Url: {}".format(i.url))
	     
	     	#BLOBS
	        for j in blob_service.list_blobs(i.name).blobs:
	            print("Blobs:")
	            print("\tNombre {}".format(j.name))
	            print("\tUrl: {}".format(j.url))
	            print("\t------------------------------")
	
