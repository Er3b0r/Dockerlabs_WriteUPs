
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20241013174042.png]]
Accedo al recurso web del puerto 80 y encuentro un formulario de login.
![[Pasted image 20241013174233.png]]
Voy a realizar un escaneo de directorios con gobuster.
Solamente encuentro el directorio `index.php` y el directorio `config.php`.
![[Pasted image 20241013175221.png]]
Voy a intentar hacer un bypass al formulario con un SQLi.
```sql
or 1-- -' or 1 or '1"or 1 or"
```
![[Pasted image 20241013175954.png]]
Encuentro al usuario `Dylan`.
![[Pasted image 20241013183235.png]]
Voy a validar el usuario y ver si encuentro alguno más que pueda pertenecer al servicio SAMBA.
Voy a utilizar `enum4linux`.
```
enum4linux 172.17.0.2
```
![[Pasted image 20241013183501.png]]
Encuentro los usuarios `augustus` y `bob` a parte del que ya sabía `dylan`.
Ahora con `crackmapexec` voy a intentar encontrar sus posibles contraseñas.
![[Pasted image 20241013184253.png]]
La contraseña que he encontrado ahí no parece servirme, así que voy a intentar obtener la contraseña del servicio ssh del usuario augustus.
![[Pasted image 20241013184653.png]]
Accedo al servicio ssh.
![[Pasted image 20241013184726.png]]
Ahora voy a intentar escalar privilegios.
![[Pasted image 20241013184954.png]]
Se me ocurre crear un `archivo.java` con una reverse shell y cuando lo ejecute, recibo una reverse shell que me dará acceso al usuario dylan.
Para ello voy a usar la herramienta online [revshells](https://www.revshells.com/).
![[Pasted image 20241013185531.png]]
Ahora ejecuto el siguiente comando para ejecutar el script que me proporciona la reverse shell.
![[Pasted image 20241013185613.png]]
Hago un tratamiento de la TTY.
```bash
script /dev/null -c bash
CTRL + z
stty raw -echo;fg
reset xterm
export TERM=xterm
exprt SHELL=bash
```
Intento escalar privilegios de nuevo.
![[Pasted image 20241013190545.png]]
![[Pasted image 20241013190848.png]]
