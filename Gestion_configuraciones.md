##Ejercicio1
###Instalar chef en la máquina virtual que vayamos a usar

Antes de instalar chef, tenemos que instalar los siguientes paquetes:

  sudo apt-get install -y ruby1.9.1 ruby1.9.1-dev rubygems
  
Y una vez instalado:

  sudo gem install ohai chef
  

##Ejercicio2
###Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

Creamos el fichero ej2.rb, que contendrá para realizar correctamente el ejercicio, lo siguiente:


Y ejecutamos chef-apply ej2.rb:

![pantallazo1]()

Ahora añadimos lo necesario para instalar nginx y un editor:



