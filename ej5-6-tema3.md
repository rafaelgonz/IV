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
###Usándolo, instalar MySql en un táper.

Antes de comenzar la explicación, indicar que en mi linux mint 15 "oliva" juju decía que era incompatible, por lo que sin perder mucho tiempo, instalé una máquina virtual ubuntu 13.10 convencional, y lo he instalado allí sin ningún tipo de problema, exceptuando este error: error: 

      error parsing environment "local": no public ssh keys found
      
Que lo solucioné siguiendo la siguiente web:

http://www.electricmonk.nl/log/2013/09/27/getting-started-with-juju-no-public-ssh-keys-found-error/

![pantallazo11](https://dl.dropbox.com/s/6tiewbwuy5naikx/pantallazo11.jpg)



Para instalar juju, vamos a realizar lo siguiente:

      sudo add-apt-repository ppa:juju/stable

Actualizamos:
    
      sudo apt-get update

E instalamos lo siguiente:

      sudo apt-get install juju-core

      
Llegados a este punto, instalamos MongoDB mediante: 
      
      sudo apt-get install mongodb-server
      
E iniciamos mongo con mongod, y creamos el archivo de configuración de juju con:

      juju init
      
Y editamos ~/.juju/environments.yaml donde default: amazon lo cambiamos por:

      default: local
      
Cambiamos el tipo de tapper con: sudo juju switch local. E instalamos mysql para integrar mediawiki:

      sudo juju deploy mediawiki
      sudo juju deploy mysql

Y para combinarlos...

      sudo juju add-relation mediawiki:db mysql
      
Y llegados a este punto, creamos un tapper de la siguiente forma:

      sudo juju bootstrap
      
Y para comprobar que todo está bien, probamos juju status, donde comprobamos que todo está bien:

![pantalazo12](https://dl.dropbox.com/s/d91f0nc8z0ikvxx/pantallazo12.jpg)

Añadimos otro contenedor, y volvemos a hacer juju status, y comprobamos que ha cambiado, añadiendose este contenedor:

![pantallazo13](https://dl.dropbox.com/s/nba9lgsxwfrih51/pantallazo13.jpg)





