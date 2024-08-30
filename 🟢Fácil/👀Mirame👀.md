Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240827173544.png]]
Voy al recurso web del puerto 80.
![[Pasted image 20240827173623.png]]
Hago un escaneo de directorios con gobuster.
![[Pasted image 20240827174211.png]]
Obtengo los siguientes recursos.
Una página donde a través de una API consulta el tiempo de una cuidad.
![[Pasted image 20240827174235.png]]
Una página de error de login.
![[Pasted image 20240827174349.png]]
Voy a intentar conseguir el usuario y la password para iniciar sesión con sqlmap apuntando al index.php.
![[Pasted image 20240827175654.png]]
Encuentro las siguientes bases de datos.
![[Pasted image 20240827175724.png]]
Ahora me interesa saber el contenido de la base de datos de users.
![[Pasted image 20240827175917.png]]
Encuentro la tabla usuarios.
![[Pasted image 20240827175933.png]]
Quiero saber el contenido de esa tabla.
![[Pasted image 20240827180031.png]]
Encuentro estas columnas.
![[Pasted image 20240827180106.png]]
Listo el contenido la cada columna de la siguiente manera.
![[Pasted image 20240827180256.png]]
Obtengo el siguiente resultado.
![[Pasted image 20240827180318.png]]
Ahora con los usuarios y sus contraseñas, intento iniciar sesión en el panel de login.
Si inicio sesión con cualquier usuario, me lleva a la dirección de page.php donde puedo consultar el clima de una ciudad.
El usuario con id 4 de la base de datos puede sugerir que podría haber un directorio oculto que no he logrado ver con el escaneo de directorios, por lo que voy a probar a buscarlo de manera manual introduciendo después de la dirección ip, el nombre del usuario directorio y si no encuentro nada, pruebo con el nombre de la contraseña.
Encuentro el siguiente recurso con una imagen.
![[Pasted image 20240827181801.png]]
Descargo la imagen para ver si con herramientas de esteganografía puedo obtener algo.
Con la herramienta steghide intento extraer posible información oculta.
![[Pasted image 20240827182548.png]]
Veo que tiene una contraseña, por lo que voy a intentar crackearla con la herramienta stegcracker.
Obtengo la posible contraseña.
![[Pasted image 20240827182914.png]]
Vuelvo a utilizar la herramienta steghide.
Obtengo un archivo llamado ocultito.zip.
![[Pasted image 20240827183035.png]]
Intento descomprimirlo pero también tiene contraseña por lo que voy a usar john the ripper para crackerarla.
![[Pasted image 20240827183142.png]]
Obtengo el contenido oculto de la siguiente manera.
![[Pasted image 20240827183538.png]]
Con el usuario y la contraseña voy a intentar iniciar sesión por ssh.
![[Pasted image 20240827183637.png]]
Ahora intento escalar privilegios buscando los permisos SUID.
![[Pasted image 20240827183836.png]]
Consigo ser root gracias al binario find.
![[Pasted image 20240827184041.png]]
