##Ejercicios 7
###Destruir toda la configuración creada anteriormente
###Volver a crear la máquina anterior y añadirle mediawiki y una relación entre ellos.
###Crear un script en shell para reproducir la configuración usada en las máquinas que hagan falta.

***Para destruir toda la configuración creada, usamos:

    sudo juju remove-unit mediawiki/0 mysql/0
    
Esto no borra las máquinas, sólo las unidades, para borrar máquinas, usaríamos:

    sudo juju destroy-machine 2
    

***Para el segundo punto, podemos observar nuestro ejercicio6, donde ya realicé otra configuración, pero a modo de resumen, estos son los pasos para realizarlo:

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
  
  
*** Para realizar esta configuración, pero esta vez utilizando un script, hemos realizado lo siguiente:

