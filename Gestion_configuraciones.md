##Ejercicio1
###Instalar chef en la máquina virtual que vayamos a usar

He utilizado una máquina virtual de ubuntu, en la que para instalar chef, realizamos lo siguiente:

    curl -L https://www.opscode.com/chef/install.sh | bash
  

##Ejercicio2
###Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.


Para realizar este ejercicio, ejecutamos chef solo, y creamos el archivo receta.rb:

    directory 'carpeta/'
    file "carpeta/receta" do
        owner "rafael"
        group "rafael"
        mode 00777
        action :create
        content "Crear receta"
    end
    
Y lo ejecutamos mediante: 

    chef-apply receta.rb

![pantallazo1](https://dl.dropbox.com/s/myhzh6ns7k48yct/pantallazo1.png)


Añadimos los paquetes de geany y nginx, tal y como nos pide el ejercicio,  volvemos a ejecutar:

    package 'nginx' 
    package 'geany

![pantallazo2](https://dl.dropbox.com/s/2jy4crci38snu4f/pantallazo2.png)



##Ejercicio3
### Escribir en YAML la siguiente estructura de datos en JSON { 'uno': 'dos', 'tres': [ 4, 5, 'Seis', { 'siete': 8, 'nueve': [Object] } ] }
