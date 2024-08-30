Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240830183501.png]]
Realizo un escaneo de directorios con gobuster.
![[Pasted image 20240830184321.png]]
Encuentro una página de login.
![[Pasted image 20240830184514.png]]
Voy a utilizar la herramienta sqlmap para intentar descubrir los datos de la base de datos de la web.
![[Pasted image 20240830184815.png]]
Encuentro las siguientes bases de datos.
![[Pasted image 20240830184837.png]]
Ahora me interesa saber el contenido de la base de datos de users.
![[Pasted image 20240830185023.png]]
Encuentro la tabla usuarios.
![[Pasted image 20240830185042.png]]
Quiero saber el contenido de esa tabla.
![[Pasted image 20240830185139.png]]
Encuentro estas columnas.
![[Pasted image 20240830185216.png]]
Listo el contenido la cada columna de la siguiente manera.
![[Pasted image 20240830185323.png]]
Obtengo el siguiente resultado.
![[Pasted image 20240830185446.png]]
Utilizo el usuario pepe y su password para iniciar sesión en la máquina a través del ssh.
Intento escalar privilegios.
Utilizo el binario grep para leer la contraseña haseada de root.
![[Pasted image 20240830192033.png]]
El hash es un md5. [(MD5 Decrypt)](https://www.md5online.org/md5-decrypt.html#google_vignette)
![[Pasted image 20240830192333.png]]
Inicio sesión como root.
![[Pasted image 20240830192433.png]]