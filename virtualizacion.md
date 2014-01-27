##Ejercicio 1
###Instalar los paquetes necesarios para usar KVM. Se pueden seguir estas instrucciones. Ya lo hicimos en el primer tema, pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.

Aunque ya lo comprobamos, volvemos a comprobar que nuestro procesador soporta la virtualización:

    egrep -c '(vmx|svm)' /proc/cpuinfo

     kvm-ok
     
![pantallazo1](https://dl.dropbox.com/s/mlc9w74gdd4u3x7/pantallazo1.png)     
     
El resultado no puede ser 0, y en lo segundo, indicar que esta preparado para usarse.

Una vez comprobado esto, vamos a instalar los paquetes necesarios, mediante:

    sudo apt-get install qemu-kvm qemu-system libvirt-bin virtinst virt-manager



##Ejercicios 2
###1. Crear varias máquinas virtuales con algún sistema operativo libre, Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar CoreOS (que sirve como soporte para Docker) GALPon Minino, hecha en Galicia para el mundo, Damn Small Linux, SliTaz (que cabe en 35 megas) y ttylinux (basado en línea de órdenes solo).


###1º máquina virtual:

Lo primero que hay que hacer es activar el módulo del kernel de VKM:

    sudo modprobe kvm-intel
    
Vamos nos descargamos la imágen de http://www.slitaz.org/en/get/#stable y creamos el disco duro virtual:

![pantallazo2](https://dl.dropbox.com/s/f0xpgi6kcmx53r3/pantallazo2.png)

Y para finalizar: 

    qemu-system-x86_64 -hda ./SliTar.img -cdrom slitaz-4.0.iso

![panallazo3](https://dl.dropbox.com/s/vsdvim8p50mblwl/pantallazo3.png)


###2º máquina virtual:


Vamos a intalar Galpon mínimo, hecha en Galicia para el mundo, descargando la imágen en http://minino.galpon.org/descargas, y creamos el disco duro virtual:


    qemu-img create -f raw galpon.img 100M
    
    qemu-system-x86_64 -hda ./SliTar.img -cdrom /Descargas/slitaz-4.0.iso

![pantallazo4](https://dl.dropbox.com/s/u9rfa8xd95ip0jn/pantallazo4.png)


###2. Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.

Instalamos VirtualBox con:
    
    apt-get install virtualbox
    
Abrimos la aplicación, y vamos a instalar SliTar:

![pantallazo5](https://dl.dropbox.com/s/5vgq6ou34t22gvh/pantallazo5.png)

![pantallazo6](https://dl.dropbox.com/s/qriyo6nn14w97e9/pantallazo6.png)

![pantallazo7](https://dl.dropbox.com/s/7nqotzcn8fvxafr/pantallazo7.png)

Y finalmente añadimos la ISO:

![pantallazo8](https://dl.dropbox.com/s/z3no3jywx6snjfa/pantallazo8.png)

Para terminar, ejecutamos nuestra máquina virtual:

![pantallazo9](https://dl.dropbox.com/s/qyqljhy4f7zc308/pantallazo9.png)



##Ejercicio3
###Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual simplemente con qemu-system-x86_64 -hda /media/Backup/Isos/discovirtual.img

Para este ejercicio, he reciclado, un benchmark en c++ que había echo el año pasado:

    #include <iostream>
    #include <cmath>
    
    using namespace std;
    
    void proceso(void) {
    	
    	unsigned int i=0;
    	unsigned int j=0;
    	unsigned int k=0;
    	
    	for(i=0; i<10000; i++){
    		for(j=0; j<10000; j++){
    			k*=13; k/=11;
    		}
    	}
    }
    
    int main(int argc, char **argv) {
    	
    	double inicio, fin;
    	
    	inicio = clock();
    	proceso();
    	fin = clock();
    	
    	double resultado = fin - inicio;
    	cout << "El tiempo es: " << resultado << endl;
    	
    	return 0;
    }

De modo, que vamos a ejecutarlo primero en lubuntu (512 MB) de virtualbox, y luego en la máquina lubuntu (512 MB( que hemos creado para el ejercicio4:

* Lubuntu - Virtualbox

![pantallazo](https://dl.dropbox.com/s/pag964dds7qylpo/pantallazo31.png)

* Lubuntu - QEMU

![pantallazo](https://dl.dropbox.com/s/51ejzlecqotvigx/pantallazo32.png)

En mi opinión, es más eficiente y he obtenido mejores resultados con la máquina de virtual box.


##Ejercicio4
###Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh

Voy a usar una imágen algo antigua de lubuntu 12.05, de modo que hacemos lo siguiente:

Creamos la máquina con virtualbox:

    qemu-img create -f qcow2 lubuntu.img 15G
    qemu-system-x86_64 -hda ~/qemu/lubuntu.img -cdrom ~/qemu/lubuntu-12.04-desktop-i386.iso -m 512M

![pantallazo10](https://dl.dropbox.com/s/63oxvbsmy5sm9er/pantallazo10.png)

Instalamos lubuntu en el sistema (pudo tardar hora y media en instalarse...), y arrancamos dentro de VNC:

    qemu-system-x86_64 -boot order=c -drive file=~/lubuntu.img,if=virtio -m 512M -name lubuntu -vnc :1
    
Luego instalamos un cliente VNC, por ejemplo Vinage, mediante:

    sudo apt-get install vinagre
    
Y seguidamente, miramos la interfaz NAT para conectarnos, con ifconfig virbr0, y nos conectamos a la máquina, mediante:

    vinagre 192.168.122.1:5901 &

![pantallazo11](https://dl.dropbox.com/s/464jh9hb2d40pgl/pantallazo11.png)


---

Para conectarnos con ssh, iniciamos la máquina, mediante:

    qemu-system-x86_64 -boot order=c -drive file=~/lubuntu.img,if=virtio -m 512M -name lubuntu -redir tcp:2222::22
    
Y en otro terminal:

    ssh -p 2222 rafael@localhost
    



##Ejercicio5
###Crear una máquina virtual ubuntu e instalar en ella un servidor nginx para poder acceder mediante web.

Instalamos una máquina ubuntu server 12-04 mediante windows azure, con un núcleo y 1,75 GB de memoria:
 
![pantallazo12](https://dl.dropbox.com/s/slczqwql5e7bhpb/pantallazo1.png)

Y nos conectamos por ssh:

![pantallazo13](https://dl.dropbox.com/s/bweeonagdgy06h5/pantallazo3.png)

Instalamos nginx mediante:

    sudo apt-get isntall ngingx

Reiniciamos el servicio:

    sudo service nginx restart

Añadimos un extremo en azure:

![pantallazo15](https://dl.dropbox.com/s/ox3j6z8pr8950dl/pantallazo15.png)
    
Y comprobamos que funciona:

http://ivubuntu.cloudapp.net

![pantallazo16](https://dl.dropbox.com/s/xv97us1daquudzq/pantallazo16.png)


##Ejercicio6
###Usar juju para hacer el ejercicio anterior.

He sacado los contenidos de: http://askubuntu.com/questions/288769/how-do-i-configure-juju-for-use-on-azure

Comenzamos con:

    sudo juju init

Y creamos lo siguiente:
    
    openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout azure.pem -out azure.pem
    openssl x509 -inform pem -in azure.pem -outform der -out azure.cer
    chmod 600 azure.pem
    
![pantallazojuju](https://dl.dropbox.com/s/omjib7cdadbxe45/pantallazojuju.png)

Para editar environmets.yaml, vamos a buscar los siguientes datos que necesitamos:

* El management-subscription-id se conoce utilizando el siguiente comando:

    azure account list

![pantallazojuju2](https://dl.dropbox.com/s/6k9xkdbrygg0rdy/pantallazojuju2.png)   
    
* El storage-account-name:

    azure storage account list
    
![pantallazojuju3](https://dl.dropbox.com/s/bdz4xca4bugsfd4/pantallazojuju3.png)

Y editamos dicho fichero, quedando de la siguiente forma:

![pantallazojuju7]()


Para subir el certificado, nos vamos a la sección "CONFIGURACIÓN" y una vez dentro a "CERTIFICADOS DE ADMINISTRACIÓN", pulsamos el botón de la parte inferior "CARGAR" y seleccionamos el nuestro archivo "azure.cer". 

![pantallazojuju4](https://dl.dropbox.com/s/b0nkdgpp78ox0fb/pantallazojuju4.png)

Llegados a este punto, creamos un taper para instalar los servicios dentro de el:

    sudo juju switch azure
    sudo juju bootstrap
    sudo juju deploy --to 0 juju-gui
    sudo juju expose juju-gui

Nos metemos en la web que nos ofrece juju status,y nos identificamos:
(La contraseña, viene en environments.yaml, como admin-secret)

![pantallazojuju6](https://dl.dropbox.com/s/mfs9ixby194ws1w/pantallazojuju6.png)

De modo que introducimos en el buscador nginx y pinchamos en añadir, y ya lo tendremos.


![pantallazojuju5](https://dl.dropbox.com/s/k53udyaoxqa6wud/pantallazojuju5.png)



##Ejercicio7
###Instalar una máquina virtual Ubuntu 12.04 para el hipervisor que tengas instalado.

Primero instalamos los siguientes paquetes:

    sudo apt-get install ubuntu-vm-builder kvm virt-manager

Y ahora decimos la distribución, destino, nombre... mediante:

    sudo vmbuilder kvm ubuntu --suite precise --flavour server -o --dest ~/iv --hostname rafael --domain rafael 

![pantallazo17](https://dl.dropbox.com/s/stfixa7nt4lu6jv/pantallazo17.png)

Y ahora, vamos a virtualBox, creamos una máquina, y cuando lleguemos a la fase donde elegimos el disco, seleccionamos lo creado anteriormente:

![pantallazo18](https://dl.dropbox.com/s/by11pjbc8o00pps/pantallazo18.png)
