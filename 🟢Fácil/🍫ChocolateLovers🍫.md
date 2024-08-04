Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240712225729](https://github.com/user-attachments/assets/daead06d-03b4-4c15-9482-35dab9dc12fa)

Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.

No logro encontrar nada.

![Pasted image 20240712230639](https://github.com/user-attachments/assets/1e60a914-f323-4ffb-b869-08e377d6ea4e)

Si accedo al código fuente del index, veo que hay comentado lo que parece ser un directorio.

![Pasted image 20240712230548](https://github.com/user-attachments/assets/386cb478-0f46-4a4a-9434-29a5a71528c8)

Entro en el directorio y me encuentro el siguiente contenido.

![Pasted image 20240712230729](https://github.com/user-attachments/assets/ebf58faf-61ba-47b6-8220-6c4da60fe02e)

Si accedo al área de admin.php, me encuentro con un formulario.

Pruebo el usuario admin y la password admin ya que son credenciales que si no se cambian suelen venir por defecto.

![Pasted image 20240712231125](https://github.com/user-attachments/assets/b4cde8b2-1d6a-4410-a3bc-2f5a31508369)

Consigo acceso y me encuentro el panel de administración de la página.

![Pasted image 20240712233330](https://github.com/user-attachments/assets/9808dfcc-883f-495f-80f9-6679e8f6c5e4)

Busco en el apartado de plugins alguno que me permita subir algún tipo de archivo para poder subir un archivo y poder generarme una reverse shell.

El plugin Image me permite hacer esto.

![Pasted image 20240712234746](https://github.com/user-attachments/assets/441dbd4f-837f-4adf-a84e-bba4cfb09520)

Con el uso de la herramienta online [Reverse Shell Generator](https://www.revshells.com/), utilizo un código de PHP PentestMonkey para generar la reverse shell.

Creo el archivo reverseshell.php y pego el código ahí.

Me pongo en escucha por el puerto que he indicado utilizando netcat.

![Pasted image 20240712235108](https://github.com/user-attachments/assets/bdd302af-13a7-4ef2-be7c-6f63758410b0)

Subo el archivo y guardo los cambios.

![Pasted image 20240712235154](https://github.com/user-attachments/assets/bf0b26e9-9f6d-425e-ae91-9f093c2b7753)

Investigando un poco, encuentro que el archivo no se ha subido, así que voy a probar a cambiarle el nombre por el de image.php para ver si se logra subir correctamente.

![Pasted image 20240712235902](https://github.com/user-attachments/assets/5db4ba65-59da-45fd-977c-2adc0ac795e6)

Ahora si que se ha guardado, debe de ser porque sustituye el contenido de image.php que ya se encontraba ahí ya que seguramente haya algo detrás que solo guarde archivos con ese nombre.

Una vez subido, accedemos al recurso y ganamos acceso a través de una reverse shell.

![Pasted image 20240713000309](https://github.com/user-attachments/assets/94a51bec-7d20-4bc4-825e-41dcaaaa96f7)

Hago un tratamiento de la tty para una mejor utilización de la consola.

```bash
script /dev/null -c bash
stty raw -echo;fg
reset
export XTERM=xterm
export SHELL=bash
```

Veo que hay un usuario con un directorio home llamado chocolate.

![Pasted image 20240713000936](https://github.com/user-attachments/assets/8ecb86c7-3004-4a3b-9027-4f369cecaa0a)

Voy a listar los binarios que puedo ejecutar como sudo.

Veo que puedo ejecutar /usr/bin/php como chocolate, así que

![Pasted image 20240713001024](https://github.com/user-attachments/assets/0614f869-a5cd-4bf1-a438-45b1b5b24f5f)

Ahora voy a usar la herramienta online de [GTFObins](https://gtfobins.github.io/) para intentar escalar privilegios.

```bash
sudo -u chocolate /usr/bin/php -r "system('$CMD');"
```

Voy a ver que procesos se están ejecutando.

Encuentro que root está ejecutando un proceso donde está ejecutando un script, por lo que voy a tratar de escalar privilegios por ahí.

![Pasted image 20240713002654](https://github.com/user-attachments/assets/80b9cffa-2811-443c-9fd5-d804cf3c360c)

El contenido del script es el siguiente.

![Pasted image 20240713002729](https://github.com/user-attachments/assets/a9f72bd6-2533-4040-b6c9-4149f2085763)

Puedo escalar privilegios de varias formas, puedo o bien modificar el contenido del archivo para proporcionarme una reverse shell o puedo hacer que root que es el que está ejecutando el script, de permisos de SUID a la bash, de forma que al ejecutarla con el parámetro -p, me proporcione una bash como root.

Voy a realizarlo de la segunda forma.

```bash
echo '<?php exec("chmod u+s /bin/bash");  ?>' > script.php
```

![Pasted image 20240713004753](https://github.com/user-attachments/assets/64c21f8e-8916-421a-ac15-44c98fbb743a)
