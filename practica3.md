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



###1º PRUEBA

    S.O -> Ubuntu server 13.10
    Configuración: 1 núcleo,  1.75 GB
    

-PANTALLAZO 1

-PANTALLAZO 2

Nos conectamos mediante SSH:

-PANTALLAZO 3

Ahora instalamos apache y git, tal y como hemos explicado al principio de esta práctica, y nos descargamos el repositorio de prácticas, para tener la aplicación que vamos a probar:



-pantallazo 4

y movemos los ficheros en cuestión a /var/www/ y mediante curl, comprobamos la página php:

-pantallazo 5

Y ya sólo falta...


        azureuser@ivubuntu1:/var/www$ ab -n 1000 -c 5 http://127.0.0.1/calculadora.php 
        This is ApacheBench, Version 2.3 <$Revision: 1430300 $> 
        Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/ 
        Licensed to The Apache Software Foundation, http://www.apache.org/ 
        
        Benchmarking 127.0.0.1 (be patient) 
        Completed 100 requests 
        Completed 200 requests 
        Completed 300 requests 
        Completed 400 requests 
        Completed 500 requests 
        Completed 600 requests 
        Completed 700 requests 
        Completed 800 requests 
        Completed 900 requests 
        Completed 1000 requests 
        Finished 1000 requests 
        
        
        Server Software:        Apache/2.4.6 
        Server Hostname:        127.0.0.1 
        Server Port:            80 
        
        Document Path:          /calculadora.php 
        Document Length:        3109 bytes 
        
        Concurrency Level:      5 
        Time taken for tests:   0.285 seconds 
        Complete requests:      1000 
        Failed requests:        0 
        Write errors:           0 
        Total transferred:      3332000 bytes 
        HTML transferred:       3109000 bytes 
        Requests per second:    3502.73 [#/sec] (mean) 
        Time per request:       1.427 [ms] (mean) 
        Time per request:       0.285 [ms] (mean, across all concurrent requests) 
        Transfer rate:          11397.54 [Kbytes/sec] received 
        
        Connection Times (ms) 
                      min  mean[+/-sd] median   max 
        Connect:        0    0   0.1      0       1 
        Processing:     0    1   0.3      1       5 
        Waiting:        0    1   0.3      1       5 
        Total:          1    1   0.3      1       5 
        
        Percentage of the requests served within a certain time (ms) 
          50%      1 
          66%      1 
          75%      1 
          80%      1 
          90%      1 
          95%      2 
          98%      2 
          99%      2 
         100%      5 (longest request) 

