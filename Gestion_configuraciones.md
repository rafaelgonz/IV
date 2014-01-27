##Ejercicio1
###Instalar chef en la máquina virtual que vayamos a usar

He utilizado una máquina virtual de ubuntu, en la que para instalar chef, realizamos lo siguiente:

    curl -L https://www.opscode.com/chef/install.sh | bash
  

##Ejercicio2
###Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.


Para realizar este ejercicio,  creamos el archivo receta.rb:

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
### Escribir en YAML la siguiente estructura de datos en 
        
        JSON { 'uno': 'dos', 'tres': [ 4, 5, 'Seis', { 'siete': 8, 'nueve': [Object] } ] }
    
    
YAML es un formato de serialización de datos legible por humanos inspirado en lenguajes como XML, C, Python, Perl, así como el formato para correos electrónicos especificado por el RFC 2822. 

A comienzos de su desarrollo, YAML significaba "Yet Another Markup Language"  para distinguir su propósito centrado en los datos en lugar del marcado de documentos. Sin embargo, dado que se usa frecuentemente XML para serializar datos y XML es un auténtico lenguaje de marcado de documentos, es razonable considerar YAML como un lenguaje de marcado ligero.
    
[Fuente: Wikipedia](http://es.wikipedia.org/wiki/YAML)

    --- # 
      tres:
        - 4
        - 5
        - "Seis"
        -
          siete: 8
          nueve:
            - "Object"
      uno: "dos"
    
    ---
    

##Ejercicio4
###Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

Comenzamos creando una máquina virtual en azure, para poder instalar allí todo lo que necesitamos para ejecutar nuestra aplicación de DAI, que se puede descargar en el siguiente enlace:

[Práctica DAI](https://www.dropbox.com/sh/zoqse981o6dp94w/rC3tLxIsRP)

![pantallazo3](https://dl.dropbox.com/s/x9rxg9vchegu2r4/pantallazo3.png)

Nos metemos por SSH, e instalamos ansible:

1.  Instalamos su repositorio:

        sudo add-apt-repository ppa:rquillo/ansible
    
2.  Terminamos la instalación:

        sudo apt-get update
        sudo apt-get install ansible
        
Una vez llegados a este punto,

