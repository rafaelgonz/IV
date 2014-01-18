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




###2. Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.

Instalamos VirtualBox con:
    
    apt-get install virtualbox
    
Abrimos la aplicación, y vamos a instalar SliTar:

![pantallazo5](https://dl.dropbox.com/s/5vgq6ou34t22gvh/pantallazo5.png)

![pantallazo6](https://dl.dropbox.com/s/qriyo6nn14w97e9/pantallazo6.png)

![pantallazo7](https://dl.dropbox.com/s/7nqotzcn8fvxafr/pantallazo7.png)

Y finalmente añadimos la ISO:

![pantallazo8](https://dl.dropbox.com/s/z3no3jywx6snjfa/pantallazo8.png)





