Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240805005020.png]]
En el recurso web del puerto 80, encuentro un apartado llamado `Acceder al Backend` en el que parece ser que se ven archivos subidos. El recurso web al que he accedido se llama upload.
Puedo utilizar este recurso más adelante para ejecutar un script y que me proporcione una reverse shell.
Por ahora voy a acceder al servicio ftp.
![[Pasted image 20240805005708.png]]
Veo que tengo todos los permisos sobre el directorio upload, probablemente sea el mismo recurso que he encontrado en la web.
Voy a tratar de subir un script php que me proporcione una reverse shell.
Para ello voy a utilizar la herramienta online [revshells](https://www.revshells.com/).
Tengo que asignarle todos los permisos o por lo menos de ejecución al script.php.
![[Pasted image 20240805010117.png]]
Ahora me pongo en escucha con netcat por el puerto indicado.
![[Pasted image 20240805010212.png]]
Subo el archivo al directorio upload del servicio ftp.
![[Pasted image 20240805010302.png]]
Voy al recurso web upload y ejecuto el script.php para poder recibir una reverse shell.
![[Pasted image 20240805010335.png]]
Selecciono el archivo `script.php` y gano acceso a la máquina en el terminal donde estaba escuchando con netcat.
Ahora hago un tratamiento de la TTY.
```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```
Intento escalar privilegios para ser el usuario `pingu`.
![[Pasted image 20240926235533.png]]
Intento escalar privilegios para ser el usuario `gladys`.
![[Pasted image 20240926235825.png]]
Intento escalar privilegios para ser el usuario `root`.
![[Pasted image 20240927000955.png]]
Ahora como no puedo editar el archivo voy a añadir directamente un usuario nuevo con una password y privilegios de root.
```bash
openssl passwd password
echo 'hacker:$1$OM6nPqQf$9TzDN//UqkfWpAZY7lZhL1:0:0::/home/hacker:/bin/bash
' >> /etc/passwd
```
Ahora inicio sesión como el usuario que acabo de añadir y ya sería root.
![[Pasted image 20240927002029.png]]
