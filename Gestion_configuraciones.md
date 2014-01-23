##Ejercicio1
###Instalar chef en la máquina virtual que vayamos a usar

He utilizado una máquina virtual de ubuntu, en la que para instalar chef, realizamos lo siguiente:

    curl -L https://www.opscode.com/chef/install.sh | bash
  

##Ejercicio2
###Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

Ejecutamos chef-solo, y editamos json.



Ahora añadimos lo necesario para instalar nginx y un editor:

    package 'nginx' 
    package 'geany'




##Ejercicio3
###
