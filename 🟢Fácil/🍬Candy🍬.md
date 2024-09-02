Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240901123931.png]]
Accedo al recurso web del puerto 80.
![[Pasted image 20240901125243.png]]
Realizo un escaneo de directorios con gobuster.
![[Pasted image 20240901125856.png]]
Encuentro la dirección del /robots.txt en la que puedo ver en la parte de abajo un posible usuario admin y una posible password que está hasheada.
![[Pasted image 20240902013359.png]]
Deshasheo la password.
![[Pasted image 20240902013431.png]]
Con estas credenciales inicio sesión en la siguiente web.
![[Pasted image 20240902013631.png]]
No encuentro nada, pero también puedo iniciar sesión en la dirección /administrator.
![[Pasted image 20240902013745.png]]
Ahora voy a tratar de modificar el código de alguna página para intentar inyectar una reverse shell y conseguir ganar acceso desde un terminal.
![[Pasted image 20240902014039.png]]
![[Pasted image 20240902014058.png]]
Pego el código de la reverse shell y guardo los cambios.
![[Pasted image 20240902014255.png]]
Me pongo en escucha con netcat y luego entro en la siguiente dirección.
![[Pasted image 20240902014417.png]]
Una vez gano acceso hago un tratamiento de la TTY.
```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```
Intento escalar privilegios pero no encuentro la forma.
Si investigo un poco, veo que hay un archivo llamado otro_caramelo.txt en el que encuentro el usuario luisillo y una password luisillosuperpassword.
![[Pasted image 20240902015321.png]]
Intento ser el usuario luisillo.
![[Pasted image 20240902020007.png]]
Ahora intento escalar a root.
Si hago un `sudo -l` veo que puedo ejecutar el comando /bin/dd como sudo.
Con los siguientes comandos logro escribir en el archivo sudoers que el usuario luisillo pueda ejecutar cualquier comando como cualquier usuario del sistema sin necesidad de introducir una contraseña.
(En la siguiente imagen se ve los permisos de sudo -l ya cambiados por pruebas anteriores durante la resolución de la máquina.)
![[Pasted image 20240902020132.png]]
