##Ejercicio 13

###Darse de alta en algún servicio PaaS tal como Heroku, Nodejitsu u OpenShift.

Como en el próximo ejercicio, se trabaja en OpenShift, he decidido darme de alta en dicho PaaS:

https://www.openshift.com/

Create a count → https://openshift.redhat.com/app/account/new?__utma=222392261.655486696.1381573316.1381573316.1381573316.1&__utmb=222392261.2.10.1381573316&__utmc=222392261&__utmx=-&__utmz=222392261.1381573316.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=(not%20provided)&__utmv=-&__utmk=111961607



##Ejercicio 14

###Crear una aplicación en OpenShift y dentro de ella instalar WordPress.


Para ello, vamos a seguir estos pasos:

https://www.openshift.com/get-started


Instalamos los siguientes paquetes:

sudo apt-get install rubygems

_sudo gem install rhc_

Y actualizamos

_sudo 	gem update rhc_

Y  nos metemos en  rhc con el usuario y pass que conseguimos en el ejercicio anterior, y nos hace un par de preguntas como:

_Your public SSH key must be uploaded to the OpenShift server to access code._
_Upload now? (yes|no)_

_Please enter a namespace (letters and numbers only) |<none>|: _

Y ya está configurado, ahora sólo falta crear nuestra primera aplicación:

rhc app create aplicacion php-5.3

Y ya está creada, podemos visitarla en:

miaplicacion-mydomain.rhcloud.com

aplicacion-rafaelgonz.rhcloud.com


Para modificar algo en dicho fichero php, lo modificamos y para que se aprecien los cambios, realizamos lo siguiente:

rafael@rafael-K55VM ~/aplicacion/php $ git config --global user.email "rafa_1_9_9_2@hotmail.com"

rafael@rafael-K55VM ~/aplicacion/php $ git config --global user.name "rafaelgonz"

rafael@rafael-K55VM ~/aplicacion/php $ git commit -a -m 'Some commit message'
[master 9b5dfb3] Some commit message
 1 file changed, 3 insertions(+), 3 deletions(-)

rafael@rafael-K55VM ~/aplicacion/php $ git push

Y en la página aparecerán los cambios que hemos realizado.


**Para instalar WordPress...**

Nos metemos en OpenShift, my apps, introducimos login, add aplication, e instalamos WordPress siguiendo las siguientes capturas:


![captura 1](https://www.dropbox.com/s/0j6gzso7mbb0yis/captura1.gif)
![captura 2](https://www.dropbox.com/s/p4tw4e5ihu78e09/captura2.gif)
![captura 3](https://www.dropbox.com/s/3qmtxo6od4l10jd/captura3.gif)
![captura 4](https://www.dropbox.com/s/qdukniednk163h1/captura4.gif)
![captura 5](https://www.dropbox.com/s/8q8hs169zqfj94z/captura5.gif)
![captura 6](https://www.dropbox.com/s/6o73g4zzbaaomcy/captura%206.gif)

y así tendríamos nuestra aplicación con wordpress instalado y funcionando, aunque en este ejercicio sólo esta última parte era necesaria, la otra es una ampliación que hice, que corresponde con la práctica 1
