## Manteniendo módulos del núcleo

* [Dependencias entre módulos](#/7/1)
* [Paso de argumentos](#/7/2)
* [Modificación de parámetros del núcleo](l#/7/4)



## Dependencias entre módulos

* Ya se ha comentado que existen dependencias entre módulos
* Esta información la encontrado en el directorio `/lib/modules/$(uname -r)/modules.dep`
* Si no existiera el fichero podemo generarlo usando `depmod`

note:
* Module dependencies are stored in the modules.dep file, which resides in your main modules directory, /lib/modules/version, where version is the kernel version number. 
* You use depmod to work on it. Type depmod with no options as root will rebuild the modules.dep file for the modules in the current kernel’s modules directory.
* This action also occurs automatically when you install kernel modules



## Paso de argumentos (I)

* A los módulos se les puede pasar parámetros (configurarlos):
  * Desde la linea de comandos cuando se cargan
  * Mediante los ficheros `/etc/modules.conf` o `/etc/modprobe.conf` o `/etc/conf.modules`
  
``` bash
> vi /etc/modules.conf

alias sound sb
alias eth0 ne2k-pci
options eth0 irq=10
```
    
note:
The main module configuration file is /etc/modules.conf or /etc/modprobe.conf. This file
holds module aliases (that is, alternate names for modules), module options, and more. This file’s
format is surprisingly complex, but most changes can be relatively simple, as described shortly 
in “Passing Options to Kernel Modules.” Very old distributions called this file /etc/conf.modules, 
but this name has fallen out of favor.



## Paso de argumentos (II)

* Actualmente se tiende a tener un directorio denominado `/etc/modules.d` o `/etc/modprobe.d` donde tenemos pequeños ficheros de configuración

```bash
ijfviana@vagalume:/etc/modprobe.d$ ls
alsa-base.conf              blacklist-modem.conf         fglrx.conf
blacklist-ath_pci.conf      blacklist-oss.conf           oss-compat.conf
blacklist.conf              blacklist-rare-network.conf  vmwgfx-fbdev.conf
blacklist-firewire.conf     blacklist-watchdog.conf
blacklist-framebuffer.conf  dkms.conf
```

* La utilidad `modules-update` un fichero monolítico de configuración parecido a `/etc/modprobe.conf` a partir de lo contenido en `/etc/modules.d`

note:
Rather than use a monolithic /etc/modules.conf or /etc/modprobe.conf file, many modern distributions place 
smaller configuration files in the /etc/modules.d or /etc/modprobe.d directory. Sometimes a utility, such
 as modules-update, generates a .conf file from the directory, but other times the files in the subdirectory
are used directly. If you use such a distribution and want to change your module configuration, you should 
do so by editing the appropriate file in /etc/modules.d or /etc/modprobe.d or by creating a new file there.
 If you see a modules.conf or modprobe.conf file, you should then type modules-update as root.



## Modificación de parámetros del núcleo (I)

* Al núcleo se le puede pasar parámetros en el momento de la cargar mediante un  *boot loader*.
* Dinámicamente podemos cambiar los valores de estos argumentos mediante el comando `sysctl`
```bash
vagalume@ijfviana:~$  sysctl -w kernel.hostname=miequipo
kernel.hostname = miequipo
```
* Si queremos que el cambio sea permanente 
```
vagalume@ijfviana:~$ echo "kernel.hostname=miequipo" >> /etc/sysctl.conf &&  sysctl -p
```

note:
Sysctl es una herramienta que nos permite cambiar parámetros del kernel sin tener que reiniciar el sistema



## Modificación de parámetros del núcleo (II)
* La sintáxis de uso de este comando es:
```
sysctl  [ parámetro ]  variable=valor
```
* Las opciones más usadas

| Opción      |  Explicación |
|------------|--------------|
| -a         | Muestra todos los valores disponibles 
| -w         | Establece el varlor indicado
| -p         | Carga en sysctl  los valores definidos en el archivo /etc/sysctl.conf
