Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20241007012850.png]]
Accedo al recurso web del puerto 80.
![[Pasted image 20241007013029.png]]
Encuentro una web en la que puedo buscar algún producto pero la petición la envía a otra IP distinta la `20.20.20.3/process.php` por el método POST.
![[Pasted image 20241007013040.png]]
Realizo un escaneo de directorios con gobuster.
![[Pasted image 20241007014140.png]]
En la ruta `/info` encuentro lo siguiente.
![[Pasted image 20241007014209.png]]
Encuentro un posible usuario `Toni`, por lo que voy a intentar realizar fuerza bruta a la máquina utilizando hydra.
![[Pasted image 20241007014428.png]]
Con las credenciales obtenidas intento acceder a la máquina.
![[Pasted image 20241007014513.png]]
Volviendo un poco atrás y viendo de nuevo el código fuente del recurso web, veo que hay una "segunda máquina" a la que va la petición.
![[Pasted image 20241007014956.png]]
Compruebo que desde la máquina víctima, en teoría tengo acceso.
En el código fuente veo también que hay un campo llamado `CMD`, voy a intentar inyectar código mandando una petición con `curl` por `POST`.
![[Pasted image 20241007015524.png]]
Funciona pero no puedo concatenar comandos.
Voy a intentar enviarme una reverse shell a otro terminal que se encuentre escuchando con netcat.
![[Pasted image 20241007015936.png]]
![[Pasted image 20241007015954.png]]
![[Pasted image 20241007020006.png]]
Hago un tratamiento de TTY.
```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```
Intento escalar privilegios y veo que tengo permisos SUID sobre el binario curl.
![[Pasted image 20241007020351.png]]
Voy a intentar modificar el archivo `/etc/passwd` con el comando curl.
Para ello primero debo de copiar el contenido en otro archivo, quitar la primera x el usuario `root` para poder iniciar como dicho usuario sin necesidad de introducir una password.
![[Pasted image 20241007021303.png]]
Y por último debo de sustituir el archivo `/etc/passwd` original por el nuevo archivo modificado.
![[Pasted image 20241007021422.png]]