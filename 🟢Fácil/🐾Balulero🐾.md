
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240929170245.png]]
Accedo al recurso web del puerto 80 y veo la siguiente web.
![[Pasted image 20240929170710.png]]
A primera vista no veo nada por lo que procedo a hacer un escaneo de directorios con gobuster.
![[Pasted image 20240929172133.png]]
Encuentro un directorio llamado `whoami` en el que no hay nada.
![[Pasted image 20240929172149.png]]
Mirando el código fuente de la web principal, encuentro que hay un recurso llamado script.js.
Si accedo al recurso veo que en el código hay el siguiente mensaje.
![[Pasted image 20240929172305.png]]
A través del navegador accedo a la siguiente ruta y encuentro un usuario y una password.
![[Pasted image 20240929173044.png]]
Accedo a la máquina a través de ssh con las credenciales que acabo de obtener.
![[Pasted image 20240929173234.png]]
Ahora voy a intentar escalar privilegios.
Veo que puedo ejecutar archivos php como el usuario `chocolate` por lo que me creo un script en php que me proporcione una reverse shell, que al ejecutarse como chocolate me proporcione una consola en otro terminal de mi máquina atacante.
![[Pasted image 20240929173757.png]]
![[Pasted image 20240929173925.png]]
Ahora hago un tratamiento de la TTY.
```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```
Voy a intentar escalar privilegios a root.
De primeras no encuentro nada que me ayude a escalar privilegios.
Utilizo la herramienta pspy para ver si hay algún proceso o comando que se esté ejecutando.
Descargo la herramienta y la ejecuto.
```bash
cd /home/chocolate
wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.1/pspy64
chmod +x pspy64
./pspy64
```
Encuentro que root está ejecutando el script que se encuentra en `/opt/script.php`
![[Pasted image 20240930210015.png]]
Decido modificarlo ya que el usuario chocolate tiene los permisos para hacerlo.
Cambio el contenido por una reverse shell.
![[Pasted image 20240930205935.png]]
