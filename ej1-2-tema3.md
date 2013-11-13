##EJERCICIO 1
###Instala LXC en tu versión de Linux favorita.


LXC (Linux Containers) es una tecnología de virtualización en el nivel de sistema operativo (SO) para Linux. OpenVZ permite que un servidor físico ejecute múltiples instancias de sistemas operativos aislados, conocidos como Servidores Privados Virtuales (SPV o VPS en inglés) o Entornos Virtuales (EV). LXC no provee de una máquina virtual, más bien provee un entorno virtual que tiene su propio espacio de procesos y redes.

Es similar a otras tecnologías de virtualización en el nivel de SO como OpenVZ y Linux-VServer, asimismo se asemeja a aquellas de otros sistemas operativos como FreeBSD jail y Solaris Containers.

LXC se basa en la funcionalidad cgroups del Linux que está disponible desde la versión 2.6.29, desarrollada como parte de LXC. También se basa en otras funcionalidades de aislamiento de espacio de nombres, que fueron desarrolladas e integradas dentro de la línea principal del núcleo de Linux.

Fuente: http://es.wikipedia.org/wiki/LXC


![pantallazo1](https://dl.dropbox.com/s/qq84ghr6hy2or7x/pantallazo1.jpg)


##EJERCICIO 2
###Comprobar qué interfaces puente ha creado y explicarlos


He creado un primer contenedor ubuntu de la siguiente forma:


    sudo lxc-create -t ubuntu -n una-caja
    sudo lxc-start -n una-caja

Y al hacer el checkconfig, la opcion user-namespace faltaba, por lo que podríamos tener problemas, pero finalmente, hemos podido instalar sin complicaciones.

![pantallazo2](https://dl.dropbox.com/s/ywr4z2r4epe47bx/pantallazo2.jpg)

Donde:

    usuario: ubuntu / password: ubuntu


Y para ver los paquetes, procedemos con ifconfig -a, donde nos da la siguiente salida:


