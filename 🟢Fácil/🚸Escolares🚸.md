
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240811022809.png]]
Accedo al recurso http por el puerto 80.
Encuentro que es una web de una universidad.
Tiene varios apartados.
![[Pasted image 20240811023049.png]]
De primeras no encuentro nada útil, por lo que voy a realizar fuzzing web con gobuster.
![[Pasted image 20240811023733.png]]
Encuentro varias direcciones, pero la que me parece más interesante es /phpmyadmin.
Encuentro un panel de login.
![[Pasted image 20240811030611.png]]
No encuentro nada, por lo que paso a otra cosa.
Si ahora voy a la web principal al apartado de profesores, encuentro que hay uno que es el administrador de WordPress.
![[Pasted image 20240811031416.png]]
Voy a utilizar la herramienta wpscan para realizar fuerza bruta y ver si puedo obtener alguna credencial a partir del usuario luis como indica el nombre o luisillo como indica su correo.
![[Pasted image 20240811040655.png]]
Encuentro el usuario luisillo y la contraseña es Luis1981, la contraseña se encuentra en el rockyou.txt, pero también es el año de su nacimiento, por lo que es una contraseña fácil de adivinar.
![[Pasted image 20240811040719.png]]
Ahora realizo fuzzing web con gobuster a la dirección /wordpress para ver si tiene algún subdominio.
![[Pasted image 20240811040356.png]]
Encuentro el subdominio /wp-admin, pero de primeras no me lo permite.
Debo añadir la ip de la máquina y el nombre del dominio escolares.dl al archivo /etc/hosts.
El nombre del dominio es proporcionado en la url cuando intento acceder al subdominio /wp-admin.
![[Pasted image 20240811042021.png]]
![[Pasted image 20240811042039.png]]
Ahora introduzco las credenciales obtenidas.
Me encuentro lo siguiente, el panel de administrador de wordpress.
![[Pasted image 20240811042140.png]]
En el menú lateral , hay un apartado que es WP File Manager el cual me va a permitir crear o modificar un archivo.
Puedo utilizar esto para intentar subir una reverse shell.
![[Pasted image 20240811042633.png]]
He utilizado la herramienta online [revshells](https://www.revshells.com/) para crear el código de la reverse shell.
Ahora me pongo en escucha por el puerto indicado en el código con la herramienta netcat.
Busco el archivo reverse.php que acabo de crear.
![[Pasted image 20240811043304.png]]
![[Pasted image 20240811043317.png]]
Ahora hago un tratamiento de la TTY.
```bash
script /dev/null -c bash
Control + Z
stty raw -echo;fg
export TERM=xterm
export SHELL=bash
```
En el direcotrio /home encuentro un archivo llamado secret.txt que parece contener la password de la máquina de luisillo.
![[Pasted image 20240811043715.png]]
Consigo iniciar sesión como luisillo.
![[Pasted image 20240811043852.png]]
Ahora voy a intentar escalar privilegios con la herramienta online [GTFOBins.](https://gtfobins.github.io/gtfobins/awk/#sudo)
![[Pasted image 20240811044424.png]]
