Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240915195944.png]]
Me llama la atención el servicio del puerto 9090, por lo que decido acceder a él a través del navegador.
![[Pasted image 20240915200430.png]]
Encuentro un formulario de login.
Pruebo a  acceder indicando credenciales por defecto como ususario:`admin` y password `admin`
![[Pasted image 20240915203544.png]]
Si me voy al apartado de `Pulgins` veo que puedo subir un archivo .tar
![[Pasted image 20240915204015.png]]
Voy a tratar de buscar algún exploit para intentar ganar acceso a la máquina.
Con la herramienta searchsploit no encuentro nada.
Si busco en el navegador, encuentro un exploit en un repositorio de [GitHub](https://github.com/miko550/CVE-2023-32315) que me proporciona una consola interactiva con la que puedo ejecutar comandos (RCE).
![[Pasted image 20240915204950.png]]
Me clono el repositorio.
![[Pasted image 20240915205143.png]]
Subo el archivo .jar al apartado de plugins.
![[Pasted image 20240915205233.png]]
Ahora si voy al apartado de `Server` y `Server Settings`, veo en el menú de la izquierda una opción que se llama `Management Tool`.
![[Pasted image 20240915205414.png]]
Me aparece un recuadro en el que ingreso la password que indica el pligin en este caso 123.
Me aparece otra página en la que debo de seleccionar el desplegable e indicar la opción `ststem command`.
![[Pasted image 20240915205655.png]]
Me aparece una especie de input en el que si introduzco un comando la máquina lo ejecuta y proyecta su resultado.
![[Pasted image 20240915205757.png]]
Consigo listar el archivo donde se encuentran los usuarios, los apunto e intento hacer fuerza bruta para entrar por ssh.
usuarios --> pinguinacio, chocolatitochingon
Compruebo que tienen un directorio home.
![[Pasted image 20240915211554.png]]
Consigo la password de chocolatitochingon.
![[Pasted image 20240915211710.png]]
Inicio sesión por ssh.
Intento escalar privilegios.
![[Pasted image 20240915212029.png]]
Ejecuto el siguiente comando que me indica en la página [GTFOBins](https://gtfobins.github.io/gtfobins/dpkg/#sudo)
![[Pasted image 20240915212100.png]]
Hago un tratamiento de TTY.
```bash
script /dev/null -c bash
```
Soy el usuario pinguinacio.
Intento escalar privilegios.
![[Pasted image 20240915213023.png]]
Si ejecuto el script, me solicita un imput, en el que yo escribo `a[$(bash >&2)]+42`. Esto me crea una subshell con privileghios de root por lo tanto ya sería root.
![[Pasted image 20240915213854.png]]
