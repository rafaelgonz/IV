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

    sudo gem install rhc

Y actualizamos

    sudo 	gem update rhc

Y  nos metemos en  rhc con el usuario y pass que conseguimos en el ejercicio anterior, y nos hace un par de preguntas como:

    Your public SSH key must be uploaded to the OpenShift server to access code.
    Upload now? (yes|no)
    Please enter a namespace (letters and numbers only) |<none>|: 


Ahora, para instalar WordPress...

Nos metemos en OpenShift, my apps, introducimos login, add aplication, e instalamos WordPress siguiendo las siguientes capturas:

Pinchamos en WordPress y aceptamos:

![captura 1](https://dl.dropbox.com/s/0j6gzso7mbb0yis/captura1.gif)

Elegimos la URL que va a tener nuestra aplicación:

![captura 2](https://dl.dropbox.com/s/p4tw4e5ihu78e09/captura2.gif)

![captura 3](https://dl.dropbox.com/s/3qmtxo6od4l10jd/captura3.gif)


Y creamos la aplicación:


![captura 4](https://dl.dropbox.com/s/qdukniednk163h1/captura4.gif)

Y podemos observar como se ha creado nuestra aplicación.
![captura 5](https://dl.dropbox.com/s/8q8hs169zqfj94z/captura5.gif)

![captura 6](https://dl.dropbox.com/s/6o73g4zzbaaomcy/captura%206.gif)

