##PRÁCTICA 1
###Creación y despliegue de una aplicación en un PaaS


**OpenShift** es un producto de computación en la nube de plataforma como servicio de Red Hat.

Este software funciona como un servicio que es de código abierto bajo el nombre de "OpenShift Origin", y está disponible en GitHub.
Los desarrolladores pueden usar Git para desplegar sus aplicaciones Web en los diferentes lenguajes de la plataforma.

OpenShift también soporta programas binarios que sean aplicaciones Web, con tal de que se puedan ejecutar en RHEL Linux. Esto permite el uso de lenguajes arbitrarios y frameworks.
OpenShift se encarga de mantener los servicios subyacentes a la aplicación y la escalabilidad de la aplicación como se necesite.
(http://es.wikipedia.org/wiki/OpenShift)



Y para realizar la práctica vamos a usar precisamente OPenShift, y para ello, comenzamos por:

Nos metemos en https://www.openshift.com/ , nos registramos e instalamos los siguientes paquetes en nuestro terminal:

_sudo apt-get install rubygems_ 

_sudo gem install rhc_

Y acto seguido, actualizamos para tener la última versión de rhc, el cuál nos ofrecerá la posibilidad de crear nuestra aplicación:

_sudo	gem update rhc_

Y  nos metemos en  rhc con el usuario y pass que conseguimos en el ejercicio anterior, y nos hace un par de preguntas como:

Your public SSH key must be uploaded to the OpenShift server to access code. 
Upload now? (yes|no) 

Please enter a namespace (letters and numbers only) |<none>|: 


A las que respondemos dependiendo de nuestros intereses, y  ya está configurado, ahora sólo falta crear nuestra primera aplicación:

_rhc app create aplicacion php-5.3_

Una vez creada, podemos visitarla en:

_miaplicacion-mydomain.rhcloud.com_

En mi caso:

_aplicacion-rafaelgonz.rhcloud.com_


Para modificar algo en dicho fichero php, lo modificamos y para que se aprecien los cambios, realizamos lo siguiente:


(Este paso sirve para identificarnos con git, ya que anteriormente en mi caso, usé git para el repositorio de clase, y para que no haya confusión, pide los datos de usuario)


_rafael@rafael-K55VM ~/aplicacion/php $ git config --global user.email "rafa_1_9_9_2@hotmail.com"_ 

_rafael@rafael-K55VM ~/aplicacion/php $ git config --global user.name "rafaelgonz"_ 

rafael@rafael-K55VM ~/aplicacion/php $ git commit -a -m 'Some commit message' 
[master 9b5dfb3] Some commit message 
 1 file changed, 3 insertions(+), 3 deletions(-) 

_rafael@rafael-K55VM ~/aplicacion/php $ git push_


Y en la página aparecerán los cambios que hemos realizado.


Podemos descargarnos el proyecto en:  https://www.dropbox.com/home/universidad/iv/PR%C3%81CTICA%201/aplicacion




###BIBLIOGRAFÍA:

 * https://www.openshift.com/get-started

 * https://www.openshift.com/developers/php

 * https://www.openshift.com/products/architecture

 * http://12theory.wordpress.com/2012/12/03/jboss-creacion-de-una-aplicacion-openshift/


