#Práctica 3

##Rafael González Jiménez


###En la asignatura se ha visto como crear almacenamiento virtual y máquinas virtuales completas. Lo importante en una máquina virtual, desde el punto de vista de un devops, es que esté adaptada a la tarea a la que se dedica. En un entorno de desarrollo de software tendremos una máquina que se encargue de testear la aplicaciones, otra para desarrollo, una última para producción. Todas se pueden virtualizar y cada una tendrá características diferentes. Desde el punto de vista de sistemas, una máquina debe usar los recursos necesarios para su funcionamiento correcto, y ni uno más, por lo que con la flexibilidad que se tiene para el uso de memoria, número de CPUs y almacenamiento se puede diseñar una máquina con los requisitos necesarios.

###En esta práctica se hace énfasis en este proceso de diseño; los comandos necesarios para configurar una máquina se conocen, pero el que una configuración u otra sea la más adecuada depende de los conocimientos adquiridos en otras asignaturas: hace falta diseñar la carga de trabajo, probar diferentes configuraciones y justificar, finalmente, que la configuración elegida es la óptima (o al menos suficientemente buena) para una finalidad determinada.

###Se pueden usar tanto máquinas virtuales locales como máquinas en la nube como una combinación de ambas si se considera necesario. De la misma forma, se puede usar sólo una, o bien varias máquinas virtuales si se ve que por temas de seguridad o cualquier otro es más conveniente.


Vamos a desarrollar la práctica con máquinas virtuales proporcionadas por Windows Azure, conectándonos con ellas por SSH.

Hemos ejecutado la aplicación que  utilizamos en la pasada práctica, que se puede descargar en el siguiente enlace: https://github.com/rafaelgonz/Practicas/tree/master/Practica2/calculadora


Y para la configuración de las mismas, hemos realizado lo siguiente:

    1. Instalar apache: sudo apt-get install apache2
    2. Instalar git: sudo apt-get install git
    3. Clonar repositorio con web: git clone git://github.com/rafaelgonz/Practicas
    4. Mover la carpeta calculadora a /var/www con: sudo mv calculadora /var/www/
    5. Ejecutar apache benchmark con el siguiente comando:
        ab -n 1000 -c 5 http://127.0.0.1/calculadora/calculadora.php

    De modo que se solicitará la página 1000 veces de 5 en 5


Dicho esto, la batería de pruebas es la siguiente:
