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

Lo primero que hay que hacer es activar el módulo del kernel de VKM:

    sudo modprobe kvm-intel
    
Vamos a instalar ubuntu server 12.04 por el buen resultado que me dió en la pŕactica 3:

Nos bajamos la imágen y:

![PANTALLAZO 3](https://dl.dropbox.com/s/vsdvim8p50mblwl/pantallazo3.png)

Instalamos vmm y realizamos la instalación:


###2. Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.





