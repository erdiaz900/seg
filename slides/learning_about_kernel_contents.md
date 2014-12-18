## Obteniendo información del núcleo

* [uname](#/3/1)



## uname (I)

* El comando [`uname`](http://linux.die.net/man/1/uname) da información sobre el núcleo en ejecución:

```bash
ijfviana@vagalume:~$ uname -a
Linux vagalume 3.8.0-30-generic #44~precise1-Ubuntu SMP Fri Aug 23 18:32:41 UTC 2013 x86_64 x86_64 x86_64 GNU/Linux
ijfviana@vagalume:~$ uname -s
Linux
ijfviana@vagalume:~$ uname -r
3.8.0-30-generic
ijfviana@vagalume:~$ uname -n
vagalume
ijfviana@vagalume:~$ uname -v
#44~precise1-Ubuntu SMP Fri Aug 23 18:32:41 UTC 2013
ijfviana@vagalume:~$ uname -m
x86_64
ijfviana@vagalume:~$ uname -o
GNU/Linux
ijfviana@vagalume:~$ uname -p
x86_64
ijfviana@vagalume:~$
```

note:
You can obtain the most important information about the kernel via the uname command:



## uname (II)

| Corta | Larga      | Explicación |
| ------|---------------------|-------------|
| -a    | --all               | Toda la información. 
| -s    | --kernel-name       | Nombre del núcleo.
| -n    | --nodename          | Nombre del servidor.
| -r    | --kernel-release    | Versión del núcleo 
| -v    | --kernel-verion     | Información adicional del núcleo
| -m    | --machine           | Arquitectura
| -p    | --processor         | Información del procesador
| -i    | --hardware-platform | Información sobre la plataforma
| -o    | --operating-system  | Información sobre el nombre del SO
| N/A   | --help              | Ayuda
| N/A   | --version           | Versión



## uname (III)

* Mucha de la información obtenida por el comando `uname` se pude obtener consultando el directorio virtual `/proc`
```bash
ijfviana@vagalume:/proc/sys/kernel$ cat ostype 
Linux
ijfviana@vagalume:/proc/sys/kernel$ cat osrelease
3.8.0-30-generic
ijfviana@vagalume:/proc/sys/kernel$ cat version
#44~precise1-Ubuntu SMP Fri Aug 23 18:32:41 UTC 2013
``` 

note:
* The /proc directory houses a variety of files that provide information on many different Linux subsystems. 
* This directory isn’t an ordinary disk directory; it’s a virtual filesystem, meaning that it’s generated on the fly as a means of interfacing with programs and users. 
* Of particular interest to the kernel is the /proc/sys/kernel subdirectory, which contains a large number of files that enable you to view  and adjust kernel settings. 
