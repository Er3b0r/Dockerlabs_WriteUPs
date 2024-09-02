Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240831132625.png]]
Realizo un escaneo de directorios con gobuster.
![[Pasted image 20240831133313.png]]
Veo el código fuente del recurso web del puerto 80 y descubro un dominio al que no puedo acceder, por lo que lo añado al /etc/hosts.
![[Pasted image 20240831132724.png]]
Ahora ya puedo acceder.
![[Pasted image 20240831132822.png]]
Si ahora realizo un escaneo de directorios de este dominio, encuentro las siguientes direcciones y puedo ver que se trata de un WordPress.
![[Pasted image 20240831133925.png]]
En la web principal de pressenter.hl, arriba a la derecha hay un apartado "Las aventuras de pressi y su fiel hacker" en el que si accedo me lleva a un post.
![[Pasted image 20240831140010.png]]
Veo que pueden existir dos posibles usuarios, pressi y Echo.
Voy a intentar acceder como pressi al WordPress.
![[Pasted image 20240831140429.png]]
Veo que el usuario es correcto pero la password no.
Con la herramienta wpscan, voy a intentar realizar fuerza bruta para intentar obtener la password del usuario pressi.
![[Pasted image 20240831141224.png]]
Encuentro las siguientes credenciales.
![[Pasted image 20240831141242.png]]
Consigo iniciar sesión en WordPress.
![[Pasted image 20240831141321.png]]

Voy a herramientas, editor de archivos de temas, selecciono el tema a editar Twenty Twenty-Two, modifico el archivo index.php y pego el codigo para obtener una reverse shell.
![[Pasted image 20240831154747.png]]
Me pongo en escucha con netcat desde el terminal.
Voy a la siguiente URL para obtener la reverse shell.
```
http://pressenter.hl/wp-content/themes/twentytwentytwo/index.php
```
![[Pasted image 20240831154530.png]]
Hago el respectivo tratamiento de TTY.
```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```
Encuentro un archivo en /tmp que no puedo leer si no soy el usuario mysql y tambien encuentro el directorio /home/enter pero no puedo entrar si no soy el usuario enter.

Accedo al recurso /var/www/pressenter/wp-config.php.
![[Pasted image 20240831165633.png]]
Encuentro una base de datos con un user y una password.
Entro en la base de datos con esas credenciales.
Busco en wp_usernames y encuentro los datos del usuario enter.
![[Pasted image 20240831165755.png]]
Inicio sesión como el usuario enter y encuentro su flag.
![[Pasted image 20240831165901.png]]
Ahora voy a intentar escalar privilegios y ser root.
No consigo nada más que leer un archivo llamado root.txt pero no es útil.
Si intento acceder a root utilizando la password del usuario enter consigo acceso y puedo ver la flag.
![[Pasted image 20240902000359.png]]

# 🏴‍☠️Flags🏴‍☠️

Flag enter --> 4a05a7bc45edb56b1f033ca1606e176c
Flag root --> 4e4a603de810988e0842777de1d97e68
