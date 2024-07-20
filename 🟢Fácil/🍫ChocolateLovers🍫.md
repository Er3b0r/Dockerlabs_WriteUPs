
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240712225729.png]]
>Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.
>No logro encontrar nada.
![[Pasted image 20240712230639.png]]
>Si accedo al código fuente del index, veo que hay comentado lo que parece ser un directorio.
![[Pasted image 20240712230548.png]]
>Entro en el directorio y me encuentro el siguiente contenido.
![[Pasted image 20240712230729.png]]
>Si accedo al área de admin.php, me encuentro con un formulario.
>Pruebo el usuario admin y la password admin ya que son credenciales que si no se cambian suelen venir por defecto.
![[Pasted image 20240712231125.png]]
>Consigo acceso y me encuentro el panel de administración de la página.
![[Pasted image 20240712233330.png]]
>Busco en el apartado de plugins alguno que me permita subir algún tipo de archivo para poder subir un archivo y poder generarme una reverse shell.
>El plugin Image me permite hacer esto.
![[Pasted image 20240712234746.png]]
>Con el uso de la herramienta online Reverse Shell Generator, utilizo un código de PHP PentestMonkey para generar la reverse shell.
>Creo el archivo reverseshell.php y pego el código ahí.
>Me pongo en escucha por el puerto que he indicado utilizando netcat.
![[Pasted image 20240712235108.png]]
>Subo el archivo y guardo los cambios.
![[Pasted image 20240712235154.png]]
>Investigando un poco, encuentro que el archivo no se ha subido, así que voy a probar a cambiarle el nombre por el de image.php para ver si se logra subir correctamente.
>![[Pasted image 20240712235902.png]]
>Ahora si que se ha guardado, debe de ser porque sustituye el contenido de image.php que ya se encontraba ahí ya que seguramente haya algo detrás que solo guarde archivos con ese nombre.
>Una vez subido, accedemos al recurso y ganamos acceso a través de una reverse shell.
![[Pasted image 20240713000309.png]]
>Hago un tratamiento de la tty para una mejor utilización de la consola.
```bash
script /dev/null -c bash
stty raw -echo;fg
reset
export XTERM=xterm
export SHELL=bash
```
>Veo que hay un usuario con un directorio home llamado chocolate.
![[Pasted image 20240713000936.png]]
>Voy a listar los binarios que puedo ejecutar como sudo.
>Veo que puedo ejecutar /usr/bin/php como chocolate, así que
![[Pasted image 20240713001024.png]]
>Ahora voy a usar la herramienta online de GTFObins para intentar escalar privilegios.
```bash
sudo -u chocolate /usr/bin/php -r "system('$CMD');"
```
>Voy a ver que procesos se están ejecutando.
>Encuentro que root está ejecutando un proceso donde está ejecutando un script, por lo que voy a tratar de escalar privilegios por ahí.
![[Pasted image 20240713002654.png]]
>El contenido del script es el siguiente.
![[Pasted image 20240713002729.png]]
>Puedo escalar privilegios de varias formas, puedo o bien modificar el contenido del archivo para proporcionarme una reverse shell o puedo hacer que root que es el que está ejecutando el script, de permisos de SUID a la bash, de forma que al ejecutarla con el parámetro -p, me proporcione una bash como root.
>Voy a realizarlo de la segunda forma.
```bash
echo '<?php exec("chmod u+s /bin/bash");  ?>' > script.php
```
![[Pasted image 20240713004753.png]]