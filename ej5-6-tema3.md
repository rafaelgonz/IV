##Ejercicio 5

###Comparar las prestaciones de un servidor web en una jaula y el mismo servidor en un contenedor. Usar nginx.

El contenedor lo creamos con lxc, y la jaula con debootstrap, y la comparación es la siguiente:

Jaula:

Instalamos ab:

      apt-get install apache2-utils


Y probamos:
     
      ab -n 50 -c 5 http://localhost/
      
donde tenemos 50 solicitudes, y 5 el número de concurrencia de solicitudes en un mismo momento.

La salida es:

![pantallazo9](https://dl.dropbox.com/s/dlp3itl636xy92w/pantallazo9.jpg)


Ahora, ejecutamos lo mismo, pero en el contenedor creado en los ejercicios anteriores:

![pantallazo10](https://dl.dropbox.com/s/o6b14kqj0pu22zu/pantallazo10.jpg)


De estas capturas, podemos sacar que 

##Ejercicios 6

###Instalar juju.

Para instalar juju, vamos a realizar lo siguiente:

      sudo add-apt-repository ppa:juju/stable

Actualizamos:
    
      sudo apt-get update

E instalamos lo siguiente:

      sudo apt-get install juju-core

Y para tener una instalación completa, instalamos:

      sudo apt-get install juju-local
      
Tendríamos que tener instalado mongoDB, para que funcionase, cosa que tengo echa, ya que en la asignatura DAI lo usamos como Base de datos.

Una vez instalado, activamos el demonio mongod y creamos un contenedor:

sudo juju bootstrap

###Usándolo, instalar MySql en un táper.
