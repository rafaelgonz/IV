##Ejercicio1
###Instalar Ruby y usar
    ruby --version
###para comprobar la versión instalada. A la vez, conviene instalar también irb, rubygems y rdoc.


Instalamos:

        sudo apt-get install ruby
        
Y para comprobar la versión instalada:

        rafael@rafael-K55VM ~ $ ruby --version
        ruby 1.9.3p194 (2012-04-20 revision 35410) [x86_64-linux]
        
NOTA: Al instalar el paquete ruby, ya se han instalado los paquetes irb, rubygems y rdoc.


##Ejercicio2
###Crear un programa en Ruby que imprima los números desde el 1 hasta otro contenido en una variable.

El programa es:
    
        #!/usr/bin/ruby

        $i = 0
        $num = 5
        
        begin
            puts("i = #$i" )
            $i +=1
        end while $i < $num
        
Y su salida es:

![pantallazo1](https://dl.dropbox.com/s/mera0frjialp8re/pantallazo1.png)

##Ejercicio3
###¿Se pueden crear estructuras de datos mixtas en Ruby? Crear un array de hashes de arrays e imprimirlo.

Si, en ruby se puede meter cualquier estructura dentro de un array

Ejemplo:

![pantallazo2](https://dl.dropbox.com/s/1d0p0a3rcuayc2d/pantallazo2.png)

##Ejercicio4
###Crear una serie de funciones instanciadas con un URL que devuelvan algún tipo de información sobre el mismo: fecha de última modificación, por ejemplo. 

###Pista: esa información está en la cabecera HTTP que devuelve
