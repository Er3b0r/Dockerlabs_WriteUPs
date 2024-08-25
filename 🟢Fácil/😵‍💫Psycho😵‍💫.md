
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240824201642.png]]
Accedo al recurso web del puerto 80.
![[Pasted image 20240824201809.png]]
Realizo una búsqueda de directorios web con gobuster.
![[Pasted image 20240824202248.png]]
Accedo al recurso.
![[Pasted image 20240824202307.png]]
Encuentro una imagen, intento obtener algún posible dato oculto con herramientas de esteganografía pero no consigo nada.
Ahora voy a intentar hacer fuzzing con wfuzz para ver si es posible que la web sea vulnerable a un ataque LFI (Local File Inclusion) ya que en el pie de index.php aparece un mensaje de [!] ERROR [!] y me hace pensar que puedo introducir algún parámetro.
```bash
wfuzz -c --hc=404 --hw=169 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt http://172.17.0.2/index.php?FUZZ=../../../../../../../../../etc/passwd

```
![[Pasted image 20240824203712.png]]
Encuentro el parámetro `secret`.
Vuelvo al index.php e introduzco lo siguiente para poder listar el archivo con los usuarios del sistema.
```
http://172.17.0.2/index.php?secret=../../../../../../../../../../etc/passwd
```
![[Pasted image 20240824203924.png]]
Intento con hydra obtener la contraseña de los usuarios vaxei y luisillo sin suerte.
Voy a probar a obtener la clave id_rsa del usuario vaxei.
![[Pasted image 20240824205257.png]]
Ahora creo el archivo id_rsa, pego la clave en su interior y le doy permisos al archivo.
![[Pasted image 20240824205506.png]]
Intento iniciar sesión al servicio ssh utilizando el archivo id_rsa para hacerme pasar por el usuario vaxei.
![[Pasted image 20240824205628.png]]
Ahora intento escalar privilegios.
Encuentro que puedo ejecutar el binario perl como luisillo, por lo que voy a intentar escalar a ese usuario.
![[Pasted image 20240824205939.png]]
Intento escalar privilegios para ser root.
![[Pasted image 20240824210615.png]]
Veo que puedo ejecutar python como root sobre el archivo paw.py que se encuentra en el directorio /opt.
Listo el contenido para ver qué es lo que hace el script.
![[Pasted image 20240824210636.png]]
A simple vista no veo que haga nada útil por lo que lo intento ejecutar.
![[Pasted image 20240824210652.png]]
AL ejecutar el script, veo que llama a un archivo llamado subprocess, pero este no existe, por lo que se me ocurre crear un archivo con ese nombre y en su interior cambiar los permisos de la bash para que cualquier usuario pueda ejecutarla como root.
![[Pasted image 20240824210912.png]]