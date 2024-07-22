
---
>Escaneo de puertos y servicios utilizando nmap.
![[Pasted image 20240722220922.png]]
>Voy al navegador y voy a la dirección 172.17.0.2:80.
![[Pasted image 20240722221119.png]]
>El contenido del archivo backup.txt es el siguiente.
![[Pasted image 20240722221149.png]]
>Me dice que el usuario es mateo y la contraseña esta cifrada posiblemente con el cifrado César.
>Voy a utilizar una herramienta online para obtener el posible descrifrado.
![[Pasted image 20240722221809.png]]
>Ahora voy a acceder a la dirección https://172.17.0.2:443.
![[Pasted image 20240722221915.png]]
>Voy a aplicar fuzzing web con la herramienta dirb.
![[Pasted image 20240722222500.png]]
>Encuentro el directorio uploads, que es donde se van a subir los archivos que suba desde el index.html.
![[Pasted image 20240722222542.png]]
>Voy a intentar subir un archivo llamado reverse1.php para ver si me puede generar una reverse shell y poder así ganar acceso al sistema.
>Hago uso de la herramienta online [revshells](https://www.revshells.com/) para crear un script que me genere la reverse shell en php.
![[Pasted image 20240722224446.png]]
>Creo el archivo, le subo, creo el servidor con Netcat para recibir la reverse shell y abro el archivbo reverse1.php para obtener la reverse shell y ganar así acceso a la máquina.
![[Pasted image 20240722224427.png]]
>Voy a hacer un tratamiento de la tty.
```bash
script /dev/null -c bash
CTRL + z
stty raw -echo;fg
reset xterm
export TERM=xterm
exprt SHELL=bash
```
>Ahora voy a intentar iniciar sesión como el usuario mateo que me han dado antes y como contraseña voy a probar easycrxazy y también easycrazy ya que creo que la que he obtenido por algún casual está mal y pienso que será la segunda opción.
![[Pasted image 20240722225345.png]]
>Consigo logearme como mateo con la contraseña easycrazy.
>Compruebo algunos directorios por si hubiese algo de contenido.
![[Pasted image 20240722225524.png]]
>Como no encuentro nada listo los binarios para ver si hay alguno que pueda ejecutar como sudo y poder escalar privilegios.
>Encuentro que puedo ejecutar /usr/bin/php, por lo que con ayuda de la herramienta online [GTFOBins](https://gtfobins.github.io/gtfobins/php/#sudo), voy a intentar escalar privilegios y convertirme en root.
![[Pasted image 20240722230052.png]]
