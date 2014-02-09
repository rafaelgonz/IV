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

[Práctica DAI](https://github.com/rafaelgonz/DAI.git)

![pantallazo3](https://dl.dropbox.com/s/x9rxg9vchegu2r4/pantallazo3.png)

Ahora en nuestra máquina local, instalamos ansible:

1.  Instalamos su repositorio:

        sudo add-apt-repository ppa:rquillo/ansible
    
2.  Terminamos la instalación:

        sudo apt-get update
        sudo apt-get install ansible
        
Una vez llegados a este punto, instalamos git en la máquina azure, mediante:

    sudo apt-get install git

En nuestra máquina local, creamos el fichero ansible_hosts e introducimos lo siguiente:

    [azure]
    rafaelDAI.cloudapp.net

Así que ya sólo queda descargar el repositorio mediante ansible, de la siguiente manera:

    
1.  Exportamos el fichero creado anteriormente:

        export ANSIBLE_HOSTS=~/ansible_hosts
        
2.  Desplegamos la aplicación:
      
        ansible azure -m git --ask-pass -u azureuser -a "repo=https://github.com/rafaelgonz/DAI.git dest=~/DAI version=HEAD"

![pantallazo4](https://dl.dropbox.com/s/41p74sbfbtz5j4h/pantallazo4.png)

Comprobamos que se ha realizado correctamente:

![pantallazo5](https://dl.dropbox.com/s/qq0ag6kq5oe1zbs/pantallazo5.png)


##Ejercicios5
###Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.


Para este ejercicio, creamos un fichero ej5.yml con la siguiente información:

    ---
    - hosts: azure
      sudo: yes
      tasks:
        - name: librerias de Python y EasyInstall
          apt: name=build-essential state=present
          apt: name=python-dev state=present
          apt: name=python-setuptools state=present
        - name: bd de MongoDB
          apt: name=mongodb-server state=present
        - name: servicios de internet, css, webpy y mako
          command: easy_install web.py mako pymongo feedparser tweepy 
        - name: ejecutar
          command: chdir=/home/DAI/Práctica4/ python formulario.py 8080 &
          async: 50
          poll: 0

Y lo ejecutamos:

    ansible-playbook ej5.yml -u azureuser --ask-pass
    
![pantallazo6](https://dl.dropbox.com/s/93s2aiomftp6i11/pantallazo6.png)


###¿Ansible o Chef? ¿O cualquier otro que no hemos usado aquí?.

En mi experiencia, puedo decir que me ha resultado más fácil, con más documentación, más flexible...  ya que chef sólo me dió problemas en los ejercicios que teníamos que hacer, y al contrario, con ansible no he tenido ningún problema.

Y lo bonito que es... jejej 

![pantallazo6](https://dl.dropbox.com/s/93s2aiomftp6i11/pantallazo6.png)



##Ejercicio6
###Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

He tenido problemas para hacerlo en mi linux mint, ya que tenía poco espacio en disco, y ahora en estas semanas no he tenido tiempo de formatearlo, así que lo he realizado en una máquina virtual, con 2 gigas de ram y 4 núcleos.


Lo primero que hacemos es instalar vagrant y  conseguir la distribución debian en [la web de vagrant](http://www.vagrantbox.es/), y:

    vagrant box add debian https://dl.dropboxusercontent.com/u/197673519/debian-7.2.0.box
    
![pantallazo7](https://dl.dropbox.com/s/qjn9p0hl0pkuq64/1.png)

Y para crear el fichero de coniguración Vagrantfile:

    vagrant init debian


Llegados a este punto, iniciamos vagrant con:

    vagrant up
    
![pantallazo9](https://dl.dropbox.com/s/tpf7i1at9tifav9/2.png)

Y ya tenemos la máquina funcionando, y nos podemos conectar por ssh con:

    vagrant ssh

![pantallazo10](https://dl.dropbox.com/s/9qlty6v0j7mhp83/3.png)


##Ejercicio7
###Crear un script para provisionar `nginx` o cualquier otro servidor web que pueda ser útil para alguna otra práctica.

Lo que tendríamos que hacer, es volver a editar el fichero VagrantFile, indicandole, que queremos instalarle a nuestra máquina nginx, de modo que añadiríamos las siguientes líneas:

    config.vm.instalacion "shell",
    inline: "sudo apt-get update && sudo apt-get install -y nginx && sudo service nginx restart && sudo service nginx status"

Y en el terminal:

    vagrant instalacion
    
![pantallazo11](https://dl.dropbox.com/s/4t162e10ztddlvr/4.png)


##Ejercicio8
###Configurar tu máquina virtual usando vagrant con el provisionador ansible.

Lo primero es darle una dirección IP a nuestra máquina, mediante:

    config.vm.network :private_network, ip: "192.168.2.50"
    
y recargamos la configuración del VagrantFile:

    vagrant reload
    
Importamos la variable HOSTS, como hacíamos en los otros ejercicios de ansible (export ANSIBLE_HOSTS=~/ansible_hosts), y editamos el VagrantFile, quedando de la siguiente manera:

    Vagrant.configure("2") do |config|
      config.vm.box = "debian"
      config.vm.network :private_network, ip: "192.168.2.50"
    
      config.vm.provision "ansible" do |ansible| 
        ansible.playbook = "playbook.yml"
      end
    
    end
    
Ahora, creamos un fichero playbook.yml, con el siguiente contenido:

    ---
    - hosts: vagrant
      sudo: yes
      tasks:
        - name: Actualizar lista de paquetes
          apt: update_cache=yes
        - name: Instalar Nginx
          apt: name=nginx state=present

Básicamente, lo que hará es instalar nginx y actualizar la caché, y a continuación:


    vagrant up
    
![pantallazo12]()

    vagrant provision

![pantallazo13]()
