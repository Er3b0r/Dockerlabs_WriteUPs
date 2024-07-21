
---
>Escaneo de puertos y servicios.
![[Pasted image 20240722003747.png]]
>Fuzzing web con gobuster.
![[Pasted image 20240722004038.png]]
>Accedo al recurso machine.php y veo que puedo subir archivos.
![[Pasted image 20240722004213.png]]
>Voy a crear un archivos llamado reverse.php en el que mediante código php crearé una reverse shell con ayuda de la herramienta online [revshells](https://www.revshells.com/).
![[Pasted image 20240722004513.png]]
>Cuando intento subir el archivo me lleva a una página llamada upload.php en la que me dice que no puedo subir archivos que no sean .zip.
![[Pasted image 20240722004624.png]]
>Voy a probar cambiando la extensión del archivo, en vez de php voy a cambiarla por una compatible como lo es phar, y de esta manera me deja subir el archivo.
![[Pasted image 20240722005528.png]]
>Una vez subo el archivo, me pongo en escucha por el puerto 4343 con la herramienta Netcat.
>Me dirijo a la dirección 172.17.0.2/uploads y abro el archivo reverse.phar que acabo de subir, ejecutándose así la reverse shell.
![[Pasted image 20240722005606.png]]
>Ahora voy a ver los binarios para ver si puedo ejecutar alguno como sudo y poder escalar privilegios.
>Encuentro un par de binarios.
![[Pasted image 20240722010221.png]]
>Voy al directorio opt ya que a veces hay contenido útil.
>Encuentro una nota.
>La nota nos da la ruta de un archivo que se encuentra en el directorio de root.
>Para poder ver su contenido, voy a aprovecharme de los binarios anteriores y gracias a la herramienta web [GTFObins](https://gtfobins.github.io/gtfobins/grep/#sudo).
![[Pasted image 20240722010842.png]]
>Ahora voy a iniciar sesión como root con la contraseña que acabo de obtener.
![[Pasted image 20240722011155.png]]
