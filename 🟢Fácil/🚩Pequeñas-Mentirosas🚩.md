
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20241001012916.png]]
Accedo al recurso web del puerto 80.
![[Pasted image 20241001012936.png]]
De primeras no encuentro nada, por lo que voy a realizar un escaneo de directorios con `gobuster`.
![[Pasted image 20241001014112.png]]
Tampoco encuentro ningún directorio oculto.
Leyendo de nuevo la `Pista`, voy a interpretar que `A` es un usuario, por lo que voy a realizar fuerza bruta a ssh para ver si consigo acceso.
![[Pasted image 20241001014432.png]]
Pruebo las credenciales y gano acceso a la máquina.
![[Pasted image 20241001014528.png]]
En la ruta `/srv/ftp` encuentro varios archivos.
Si muestro el contenido de `hash_scpencer.txt` veo que contiene una cadena de caracteres cifrada en lo que puede ser MD5.
![[Pasted image 20241001015424.png]]
Compruebo si puedo descifrarlo con una herramienta online.
![[Pasted image 20241001015454.png]]
Si ahora muestro el contenido de `pista_fuerza_bruta.txt` me dice que pruebe a realizar un ataque de fuerza bruta al usuario `spencer`.
![[Pasted image 20241001015547.png]]
![[Pasted image 20241001015559.png]]
Veo que ambas contraseñas coinciden por lo que me imagino que el resto de archivos son pequeños retos para poder descifrar la contraseña de diferentes formas.
Voy a iniciar como el usuario `spencer`.
![[Pasted image 20241001015715.png]]
Ahora voy a intentar escalar privilegios.
![[Pasted image 20241001015831.png]]
