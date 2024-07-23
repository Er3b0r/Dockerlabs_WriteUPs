>Escaneo de puertos y servicios.

![Pasted image 20240722003747](https://github.com/user-attachments/assets/24d63b50-a1a4-4886-a937-c417a085edca)
>Fuzzing web con gobuster.

![Pasted image 20240722004038](https://github.com/user-attachments/assets/b6bd8359-e1be-4213-94fc-1f9519a98be0)
>Accedo al recurso machine.php y veo que puedo subir archivos.

![Pasted image 20240722004213](https://github.com/user-attachments/assets/5b1ef1e2-c862-45eb-94e6-b3b1b29c58b2)
>Voy a crear un archivo llamado reverse.php en el que mediante código php crearé una reverse shell con ayuda de la herramienta online [revshells](https://www.revshells.com/).

![Pasted image 20240722004513](https://github.com/user-attachments/assets/cd11fa24-12a7-40d6-bf4c-b5111d5c9026)
>Cuando intento subir el archivo me lleva a una página llamada upload.php en la que me dice que no puedo subir archivos que no sean .zip.

![Pasted image 20240722004624](https://github.com/user-attachments/assets/76b486ad-062f-4fed-a551-df59552376f7)
>Voy a probar cambiando la extensión del archivo, en vez de php voy a cambiarla por una compatible como lo es phar, y de esta manera me deja subir el archivo.

![Pasted image 20240722005528](https://github.com/user-attachments/assets/830c8c00-64f3-4bff-ad16-89c78b6f9a6a)
>Una vez subo el archivo, me pongo en escucha por el puerto 4343 con la herramienta Netcat.
>Me dirijo a la dirección 172.17.0.2/uploads y abro el archivo reverse.phar que acabo de subir, ejecutándose así la reverse shell.

![Pasted image 20240722005606](https://github.com/user-attachments/assets/ea31910f-d039-45a4-a63f-efed735fb3e5)
>Ahora voy a ver los binarios para ver si puedo ejecutar alguno como sudo y poder escalar privilegios.
>Encuentro un par de binarios.

![Pasted image 20240722010221](https://github.com/user-attachments/assets/98185940-fd8a-40d6-8611-0089966b97aa)
>Voy al directorio opt ya que a veces hay contenido útil.
>Encuentro una nota.
>La nota nos da la ruta de un archivo que se encuentra en el directorio de root.
>Para poder ver su contenido, voy a aprovecharme de los binarios anteriores y gracias a la herramienta web [GTFObins](https://gtfobins.github.io/gtfobins/grep/#sudo).

![Pasted image 20240722010842](https://github.com/user-attachments/assets/dbd8cdfb-f4f1-4478-8987-c6c639401fcd)
>Ahora voy a iniciar sesión como root con la contraseña que acabo de obtener.

![Pasted image 20240722011155](https://github.com/user-attachments/assets/e94354f6-bb43-4400-9a24-ae5075a549fb)
