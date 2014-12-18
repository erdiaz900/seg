## Obteniendo información de los módulos

* [lsmod](#/4/1)
* [modinfo](#/4/2)



## lsmod

* Podemos obtener información de los módulos cargamos mediante el comando [`lsmod`](http://linux.die.net/man/8/lsmod)

``` bash
ijfviana@vagalume:/proc/sys/kernel$ lsmod
Module                  Size  Used by
nls_iso8859_1          12713  1 
hid_generic            12540  0 
usb_storage            61749  1 
hidp                   22599  1 
hid                   105549  2 hid_generic,hidp
acpi_call              12748  0 
nvram                  14413  0 
pci_stub               12622  1 
vboxpci                23236  0 
vboxnetadp             25670  0 
vboxnetflt             27612  1 
vboxdrv               320274  5 vboxpci,vboxnetadp,vboxnetflt
rfcomm                 47864  12 
bnep                   18258  2 
parport_pc             28284  0 
ppdev                  17113  0 
binfmt_misc            17540  1 
uvcvideo               82214  0 
videobuf2_core         40785  1 uvcvideo
videodev              130053  2 uvcvideo,videobuf2_core
```

note:
* You can learn about the modules that are currently loaded on your system by using lsmod. 
* First  column specifies the names of all the modules that are currently loaded.  
* The Used by column of the lsmod output describes what’s using the module. 
* All the entries have a number, which indicates the number of other modules or processes that are using the module. 
* El número y nombre pueden no coincidir ya que el número hace referencia también a elementos internos del núcleo que están usando el módulo.



## modinfo

* Podemos obtener más información de los módulos cargados usando el comando [`modinfo`](http://linux.die.net/man/8/modinfo)

```bash
ijfviana@vagalume:/proc/sys/kernel$ modinfo lp
filename:       /lib/modules/3.8.0-30-generic/kernel/drivers/char/lp.ko
license:        GPL
alias:          char-major-6-*
srcversion:     0946BE622F5ED3946F6D2AA
depends:        parport
intree:         Y
vermagic:       3.8.0-30-generic SMP mod_unload modversions 
parm:           parport:array of charp
parm:           reset:bool
ijfviana@vagalume:/proc/sys/kernel$ modinfo -Flicense lp
GPL
```

note:
* You can learn still more about kernel modules with the help of the modinfo command.  
* The information returned usually includes the filename, its license name, aliases by which it’s known, a brief description, the names of any modules upon which it depends, some kernel version information, and parameters that can be passed to the module. 
* If you’re interested in only one field, you can specify it with the -Ffieldname option,
