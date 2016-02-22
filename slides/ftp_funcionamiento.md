## FTP

* [ACTIVO](#/4/1)
* [PASIVO](#/4/2)



## ACTIVO

* El cliente envía al servidor la dirección IP y el número de puerto en el que escuchará la conexión de datos

note:
* Modo Activo: 
* 1. El cliente abre un canal de comando del puerto de cliente >1023 al puerto del servidor 21.
* 2. El cliente envía PORT 1.051 (1.050 + 1) al servidor y el servidor reconoce en el canal de comandos.
* 3.El servidor abre un canal de datos desde el puerto del servidor 20 al puerto de cliente 1051.
* 4. El cliente reconoce en el canal de datos.




## PASIVO

* El cliente envía un comando PASV al servidor y recibe una dirección IP y número de puerto a cambio. El servidor responde con PORT XXXX XXXX es el puerto no privilegiado el servidor escucha para la conexión de datos y pasivamente espera la conexión de datos.


note:
*  1.Cliente abre canal de comando de puerto de cliente 1050 al puerto del servidor 21.
*  2.El cliente envía comandos PASV al servidor en el canal de comandos.
*  3.Servidor envía de vuelta (en el canal de comandos) PORT 1234 después de comenzar a escuchar en ese puerto.
*  4.Cliente abre canal de datos desde el cliente 1050 al puerto de servidor 1234.
*  5.Servidor reconoce en el canal de datos.

