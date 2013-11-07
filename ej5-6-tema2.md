
##EJERCICIO 5
###Instalar una jaula chroot para ejecutar el servidor web de altas prestaciones nginx.

Para ejecutar nginx, vamos a utilizar el sistema instalado en el ejercicio anterior, y lo primero que tenemos que hacer es meternos como choot:

                 sudo chroot /home/Documentos

Y luego, instalamos nginx mediante:

                 apt-get install nginx

y aceptamos todas las preguntas o utilizando el que nginx nos proporciona de ejemplo.

Para comprobar el funcionamiento, instalamos curl, el cual nos permite desde consola visualizar ficheros html, como podemos obervar en el pantallazo, donde visualizamos el html de prueba de nginx:

![captura3] (https://dl.dropbox.com/s/cjp73n5zg88a7lu/pantallazo.png)


##EJERCICIO 6 
###Crear una jaula y enjaular un usuario usando jailkit, que previamente se habrá tenido que instalar.

La idea principal de jailkit es realizar una jaula de la forma más segura posible, por eso se basa en copiar sólo y exclusivamente los ficheros necesarios para ejecutar lo que se quiera ejecutar.


En la web oficial, nos bajamos el paquete, y después nos metemos en el directorio descargado, e instalamos el paquete:

              ./configure && make && sudo make install

Llegados a este punto, tenemos que crear un sistema de ficheros poseido por root, que como aparece en la documentación sería:

             mkdir -p /seguro/jaulas/dorada
             chown -R root:root /seguro

Y a partir de aquí:

             sudo jk_init -v -j /seguro/jaulas/dorada jk_lsh basicshell netutils editors

Ahora procedemos a enjaular un usuario:

1º Creamos un usuario en unix:

             sudo adduser prueba


2º Enjaulamos mediante:

             sudo jk_jailuser -m -j /seguro/jaulas/dorada prueba
s
**Bibliografía:** http://olivier.sessink.nl/jailkit/
