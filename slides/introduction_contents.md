## Introducción

<a class="fancybox" href="img/operaciones_modulos.png" data-fancybox-group="gallery" title="Operaciones con módulos">
<img height="550px" src="img/operaciones_modulos.png" alt="Operaciones con módulos">
</a>

note:
* Early Linux kernels consisted of a single file, which was loaded into memory by the boot loader. 
* Although modern kernels still use this primary kernel file, Linux has supported kernel modules for several years. 
* Placing most drivers in modules helps 
 * keep the size of the main kernel file down, 
 * enables the use of a  single “generic” kernel on many computers without bloating the kernel’s size too much, 
 * and gives users control over when and how drivers are loaded. 
* This approach does require learning something about how  modules are controlled, though. 

