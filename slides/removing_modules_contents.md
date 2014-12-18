## Descargando módulos del núcleo

* [¿Por qué descargar?](#/6/1)
* [rmmod](#/6/2)



## ¿Por qué descargar?

* Una vez cargado, los módulos se quedan en memoria indefinidamente
* Razones para descargaa el descarga un módulo de memoria son:
 * Reducción de memoria cargada
 * Inestabilidad del sistema
 * Reducir consumo de memoria

note:
In most cases, you can leave modules loaded indefinitely; the only harm that a module does when it’s loaded but
not used is to consume a small amount of memory. (The lsmod program shows how much memory each module
consumes.) Sometimes, though, you might want to remove a loaded module. Reasons include reclaiming that tiny
amount of memory, unloading an old module so that you can load an updated replacement module, and removing
a module that you suspect is unreliable.



## rmmod (I)

* Para descargar un módulo de memoria usamos el comando [`rmmod`](http://linux.die.net/man/8/rmmod)

```bash
ijfviana@vagalume:~$ sudo rmmod axnet_cs
```
* Si el módulo a desinstalar es usado por otro módulo dará error

note:
The actual work of unloading a kernel module is done by the rmmod command, which is something of the
opposite of insmod. The rmmod command takes a module name as an option, though, rather than a module
filename:



## rmmod (II)

| Carta | Larga     | Explicación |
|-------|-----------|-------------|
| -v    | --verbose | Modo detallado
| -f    | --force   | Descarga un módulo aunque otros dependan de el si el núclero fue configurado con la opción CONFIG_MODULE_FORCE_UNLOAD activakernel option is enabled.
| -w    | --wait    | Espera a que el módulo no estñe en uso antes de descargalo |
| -s    | --syslog  | Manda mensajes al logger del sistema
| -V    | --version | Muestra la versión de rmmod
