Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20241001213948.png]]
Accedo al recurso web del puerto 80.
![[Pasted image 20241001214017.png]]
Voy a realizar un escaneo de directorios con `gobuster`.
![[Pasted image 20241001214314.png]]
Encuentro que hay un directorio llamado `wordpress`.
![[Pasted image 20241001214356.png]]
Vuelvo a realizar un escaneo de directorios pero esta vez a partir de la dirección `http://172.17.0.2/wordpress/`.
![[Pasted image 20241001214614.png]]
En la web `http://172.17.0.2/wordpress/` encuentro un usuario `chocolate` que ha posteado algo.
![[Pasted image 20241001214623.png]]
No puedo acceder a ninguna de las direcciones encontradas por lo que voy a realizar fuerza bruta al ssh con el usuario que he obtenido (Si añado la ip de la máquina víctima al `/etc/hosts` y le asigno el nombre `collections.dl`, puedo acceder a un panel de login de wordpress, pero es más rápido y fácil de la siguiente forma.).
![[Pasted image 20241001215024.png]]

![[Pasted image 20241001215059.png]]
Consigo acceso pero no puedo escalar privilegios.
Decido entonces conectarme a su base de datos mongodb en el puerto 27017.
![[Pasted image 20241001220231.png]]
Encuentro el usuario `dbadmin` y su password `chocolaterequetebueno123`.
Inicio sesión con esas credenciales.
![[Pasted image 20241001220334.png]]
No encuentro la forma de escalar privilegios de nuevo, por lo que pruebo a intentar iniciar sesión como root con las contraseñas que he obtenido hasta ahora y consigo ser root con la password `chocolaterequetebueno123`.
![[Pasted image 20241001220658.png]]
