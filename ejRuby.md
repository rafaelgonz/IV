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

Mi código es:

        #!/usr/bin/ruby
    
        require 'net/http'

        def fecha()
        	response = Net::HTTP.get_response('www.alfinaldelapalmera.com','/')  	
	        return response['date'].to_s
        end

        def conexion()
        	response = Net::HTTP.get_response('www.alfinaldelapalmera.com','/')  	
        	return response['content-type'].to_s
        end

        def servidor()
	        response = Net::HTTP.get_response('www.alfinaldelapalmera.com','/')  	
	        return response['server'].to_s
        end

        puts ('fecha:') 
        puts fecha()

        puts ('tipo del contenido')   
        puts conexion()
        
        puts ('informacion del servidor:') 
        puts servidor()

Y su ejecución es:

![pantallazo3](https://dl.dropbox.com/s/9agkprllf5j3z55/pantallazo3.png)


##Ejercicio5
###Ver si está disponible Vagrant como una gema de Ruby e instalarla.

Para la instalación de vagrant, en lugar de apt-get utilizamos gem, para que sea gema de ruby, así que la buscaríamos de la siguiente forma:
	
		gem search --remote vagrant
		
y para instalarla:

		sudo gem install vagrant

Pero nos da error, así que probamos a instalar: 

		sudo apt-get install ruby-dev
		
Ahora instalamos, y todo va correctamente, ya que el paquete ruby-dev es necesario para la instalación de lsa gemas de Ruby.


