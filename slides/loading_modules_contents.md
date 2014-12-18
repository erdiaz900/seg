## Cargando módulos del núcleo

* [insmod](#/5/1)
* [modprobe](#/5/2)

note:
* Linux enables you to load kernel modules with two programs: insmod and modprobe.
* The insmod program inserts a single module into the kernel. This process requires that any modules upon which the module you’re loading relies are already loaded.
* The modprobe program, by contrast, automatically loads any depended-on modules and so is generally the preferred way to do the job.



## insmod

* El comando [insmod](http://linux.die.net/man/8/insmod) Debemos indicar la ruta completa del fichero del módulo a cargar

```bash
ijfviana@vagalume:~$ insmod /lib/modules/3.8.0-30-generic/kernel/drivers/net/ethernet/8390/axnet_cs.ko
ijfviana@vagalume:~$ lsmod | grep axnet_cs
Module          Size    Used by
axnet_cs        26072	0
```

* Podemos pasar parámetros al módulo, los consultamos en `/usr/src/linux/Documentation`

```bash
ijfviana@vagalume:/lib/modules$ insmod /lib/modules/2.6.35.4/kernel/drivers/cdrom/cdrom.ko speed=720
```

note:
In practice, insmod is a fairly straightforward program to use; you type it followed by the module filename:
# insmod /lib/modules/2.6.35.4/kernel/drivers/cdrom/cdrom.ko
This command loads the cdrom.ko module, which you must specify by filename. Modules have module names,
too, which are usually the same as the filename but without the extension, as in cdrom for the cdrom.ko file.
Unfortunately, insmod requires the full module filename, which can be tedious to type—or even to locate the file!
You can pass additional module options to the module by adding them to the command line. Module options
are highly module-specific, so you must consult the documentation for the module to learn what to pass. Examples
include options to tell an RS-232 serial port driver what interrupt to use to access the hardware or to tell a video
card framebuffer driver what screen resolution to use.



## modprobe (I)

* `insmod` tiene dos problemas
 * Es tedioso poner el camino completo de los módulos
 * No resuelve las dependencias entre módulos
* Las dependecias de los módulos las podemos consultar en `/lib/modules/$(name -r)/modules.dep`:

```bash
ijfviana@vagalume:$ grep axnet_cs /lib/modules/`uname -r`/modules.dep
kernel/drivers/net/ethernet/8390/axnet_cs.ko:
    kernel/drivers/pcmcia/pcmcia.ko kernel/drivers/pcmcia/pcmcia_core.ko
```

* Antes de cargar un módulo es necesario cargar sus dependencias

```bash
> insmod cdrom
ijfviana@vagalume:$ insmod /lib/modules/3.8.0-30-generic/kernel/drivers/pcmcia/pcmcia_core.ko
ijfviana@vagalume:$ insmod /lib/modules/3.8.0-30-generic/kernel/drivers/pcmcia/pcmcia.ko
ijfviana@vagalume:$ insmod /lib/modules/3.8.0-30-generic/kernel/drivers/net/ethernet/8390/axnet_cs.ko
```

note:
Some modules depend on other modules. In these cases, if you attempt to load a module that depends on
others and those other modules aren’t loaded, insmod will fail.



## modprobe (II)

* El comando [`modprobe`](http://linux.die.net/man/8/modprobe) soluciona estos problemas:
```bash
ijfviana@vagalume:$ modprobe axnet_cs
```
* **Es recomendable usar `modprobe` y no `insmod`**

note:
When this happens, you must either track  down and manually load the depended-upon modules or use
 modprobe. In the simplest case, you can use  modprobe just as you use insmod, by passing it a module name.



## modprobe (III)

| Short      | Long             | Explicación |
|------------|------------------|-------------|
| -v         | --verbose        | Modo detallado
| -Cfilename |-- configfilename | Cambia el fichero de configuración, por defecto es `/etc/modprobe.conf`
| -n         | --dry-run        | Realiza las comprobaciones necesarias para hacer la instalación
| -r         | --remove         | Descarga el módulo que se le indica. No toca dependencias
| -f         | --force          | Fuerza la instalación del módulo
| N/A        | --show-depends   | Muestra los módulos de los que depende el módulo que se indica
| -l         | --list           | Muestra módulos disponibles
