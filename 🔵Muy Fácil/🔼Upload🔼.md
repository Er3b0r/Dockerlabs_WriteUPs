
---
>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.
![[Pasted image 20240616203826.png]]
>El escaneo reporta un servicio http.
>Me dispongo a hacerle un fuzzing web a la dirección ip.
>Encuentro varias direcciones a las que puedo acceder, 2 index.html un directorio unpload y un archivo que se encuentra dentro llamado uploads.php.
![[Pasted image 20240619023201.png]]
>Ahora voy a utilizar un script en php y al subirlo a la página web, acceder a uploads y seleccionar el script  para proporcionarnos una reverse shell.
>Primero nos pones en escucha y luego seleccionamos el archivo subido para conseguir acceso remoto con la reverse shell.
![[Pasted image 20240619023325.png]]
![[Pasted image 20240619023240.png]]
>Una vez consigo la reverse shell, voy a hacer un tratamiento de la consola para que sea más facil utilizarla.
>Para poner una consola interactiva.
```bash
script /dev/null -c bash
Ctrl + Z
export TERM=xterm
reset
```
>Ahora voy a listar los binarios sobre los que el usuario con el que he establecido la conexión puede ejecutar como sudo sin necesidad de introducir contraseña.
>Utilizando la herramienta GTFObins, vamos a buscar un comando que nos permita escalar privilegios a root utilizando el binario /usr/bin/env
>Ejecutamos el comando y ya somos root.
![[Pasted image 20240616205515.png]]
