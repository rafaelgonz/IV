##Ejercicios 7
###Destruir toda la configuración creada anteriormente
###Volver a crear la máquina anterior y añadirle mediawiki y una relación entre ellos.
###Crear un script en shell para reproducir la configuración usada en las máquinas que hagan falta.

***
*   Para destruir toda la configuración creada, usamos:

    sudo juju remove-unit mediawiki/0 mysql/0
    
Esto no borra las máquinas, sólo las unidades, para borrar máquinas, usaríamos:

    sudo juju destroy-machine 2
    

***
*   Para el segundo punto, podemos observar nuestro ejercicio6, donde ya realicé otra configuración, pero a modo de resumen, estos son los pasos para realizarlo:

Creamos un contenedor:

    sudo juju bootstrap
  
y creamos el archivo de configuración de juju con:

     juju init
  
Editamos ~/.juju/environments.yaml donde default: amazon lo cambiamos por:

    default: local
  
Cambiamos el tipo de tapper con: sudo juju switch local. E instalamos mysql para integrar mediawiki:

    sudo juju deploy mediawiki
    sudo juju deploy mysql
  
  
Y para combinarlos...

    sudo juju add-relation mediawiki:db mysql
    juju expose mediawiki 
  
  
***
*   Para realizar esta configuración, pero esta vez utilizando un script, hemos realizado lo siguiente:

Unir todos los pasos realizados en estos ejercicios, secuenciamente en un script, de modo que cuando se ejecute, el resultado sea el mismo:

El script es:

        #!/bin/bash
        juju init
        juju switch local 
        juju bootstrap 
        juju deploy mediawiki
        juju deploy mysql 
        juju add-relation mediawiki:db mysql 
        juju expose mediawiki 
        juju status 
    
Una vez guardado con extensión .sh para ser shell, cambiamos los permisos, y como superusuario, lo ejecutamos de la siguiente forma:

    sudo ./script.sh
    

##Ejercicio 8
###Instalar libvirt. Te puede ayudar esta guía para Ubuntu.

El paquete libvirt es un API hypervisor independiente de la virtualización que es capaz de interactuar con las capacidades de virtualización de una variedad de sistemas operativos.

El paquete libvirt suministra:

Una capa común, genérica, y estable para gestionar con seguridad máquinas virtuales en un host.
Una interfaz común para gestionar los sistemas locales y los hosts en red.
Todas las APIs requeridas para provisionar, crear modificar, monitorizar, controlar, migrar y parar máquinas virtuales, pero sólo si el hypervisor soporta estas operaciones. Aunque se puede acceder a múltiples hosts con libvirt, las APIs están limitadas a operaciones de único nodo.

(http://docs.fedoraproject.org/es-ES/Fedora/18/html/Virtualization_Getting_Started_Guide/sec_libvirt-libvirt-tools.html)


Para instalar libvirt:

![pantallazo14](https://dl.dropbox.com/s/ny6bpf64x9eebh7/pantallazo14.jpg)
