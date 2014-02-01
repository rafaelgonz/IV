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


Lo primero que hacemos es instalar vagrant y  conseguir la distribución debian en [la web de vagrant](http://www.vagrantbox.es/), y:

    vagrant box add Debian2 http://tools.swergroup.com/downloads/wheezy32.box
    
![pantallazo7](https://dl.dropbox.com/s/ql3x2m2vaqq17c2/pantallazo7.png)

Y para crear el fichero de coniguración Vagrantfile:

    vagrant init IVDebian

Ahora, cambiamos el fichero Vagrantfile, quedando de la siguiente manera:

        # -*- mode: ruby -*-
        # vi: set ft=ruby :
        
        Vagrant::Config.run do |config|
          # All Vagrant configuration is done here. The most common configuration
          # options are documented and commented below. For a complete reference,
          # please see the online documentation at vagrantup.com.
        
          # Every Vagrant virtual environment requires a box to build off of.
          config.vm.box = "Debian2"
        
          # The url from where the 'config.vm.box' box will be fetched if it
          # doesn't already exist on the user's system.
          config.vm.box_url = "http://tools.swergroup.com/downloads/wheezy32.box"
        
          # Boot with a GUI so you can see the screen. (Default is headless)
          # config.vm.boot_mode = :gui
        
          # Assign this VM to a host-only network IP, allowing you to access it
          # via the IP. Host-only networks can talk to the host machine as well as
          # any other machines on the same network, but cannot be accessed (through this
          # network interface) by any external networks.
          # config.vm.network :hostonly, "192.168.33.10"
        
          # Assign this VM to a bridged network, allowing you to connect directly to a
          # network using the host's network device. This makes the VM appear as another
          # physical device on your network.
          # config.vm.network :bridged
        
          # Forward a port from the guest to the host, which allows for outside
          # computers to access the VM, whereas host only networking does not.
          # config.vm.forward_port 80, 8080
        
          # Share an additional folder to the guest VM. The first argument is
          # an identifier, the second is the path on the guest to mount the
          # folder, and the third is the path on the host to the actual folder.
          # config.vm.share_folder "v-data", "/vagrant_data", "../data"
        
          # Enable provisioning with Puppet stand alone.  Puppet manifests
          # are contained in a directory path relative to this Vagrantfile.
          # You will need to create the manifests directory and a manifest in
          # the file debian2.pp in the manifests_path directory.
          #
          # An example Puppet manifest to provision the message of the day:
          #
          # # group { "puppet":
          # #   ensure => "present",
          # # }
          # #
          # # File { owner => 0, group => 0, mode => 0644 }
          # #
          # # file { '/etc/motd':
          # #   content => "Welcome to your Vagrant-built virtual machine!
          # #               Managed by Puppet.\n"
          # # }
          #
          # config.vm.provision :puppet do |puppet|
          #   puppet.manifests_path = "manifests"
          #   puppet.manifest_file  = "debian2.pp"
          # end
        
          # Enable provisioning with chef solo, specifying a cookbooks path, roles
          # path, and data_bags path (all relative to this Vagrantfile), and adding 
          # some recipes and/or roles.
          #
          # config.vm.provision :chef_solo do |chef|
          #   chef.cookbooks_path = "../my-recipes/cookbooks"
          #   chef.roles_path = "../my-recipes/roles"
          #   chef.data_bags_path = "../my-recipes/data_bags"
          #   chef.add_recipe "mysql"
          #   chef.add_role "web"
          #
          #   # You may also specify custom JSON attributes:
          #   chef.json = { :mysql_password => "foo" }
          # end
        
          # Enable provisioning with chef server, specifying the chef server URL,
          # and the path to the validation key (relative to this Vagrantfile).
          #
          # The Opscode Platform uses HTTPS. Substitute your organization for
          # ORGNAME in the URL and validation key.
          #
          # If you have your own Chef Server, use the appropriate URL, which may be
          # HTTP instead of HTTPS depending on your configuration. Also change the
          # validation key to validation.pem.
          #
          # config.vm.provision :chef_client do |chef|
          #   chef.chef_server_url = "https://api.opscode.com/organizations/ORGNAME"
          #   chef.validation_key_path = "ORGNAME-validator.pem"
          # end
          #
          # If you're using the Opscode platform, your validator client is
          # ORGNAME-validator, replacing ORGNAME with your organization name.
          #
          # IF you have your own Chef Server, the default validation client name is
          # chef-validator, unless you changed the configuration.
          #
          #   chef.validation_client_name = "ORGNAME-validator"
        end

Llegados a este punto, iniciamos vagrant con:

    vagrant up
    
![pantallazo9](https://dl.dropbox.com/s/ccmhxwirc69rv2n/pantallazo9.png)

Y ya tenemos la máquina funcionando, y nos conectamos por ssh:

    vagrant ssh

![pantallazo10]()


##Ejercicio7
###Crear un script para provisionar `nginx` o cualquier otro servidor web que pueda ser útil para alguna otra práctica.

Lo que tendríamos que hacer, es volver a editar el fichero VagrantFile, indicandole, que queremos instalarle a nuestra máquina nginx, de modo que añadiríamos las siguientes líneas:

    config.vm.instalacion "shell",
    inline: "sudo apt-get update && sudo apt-get install -y nginx && sudo service nginx restart && sudo service nginx status"

Y en el terminal:

    vagrant instalacion
    
![pantallazo11]()


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

Básicamente, lo que hará es instalar nginx y actualizar la caché.

Comprobamos que funciona:

    vagrant provision

![pantallazo]()
