##Ejercicio 5

###Comparar las prestaciones de un servidor web en una jaula y el mismo servidor en un contenedor. Usar nginx.


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
