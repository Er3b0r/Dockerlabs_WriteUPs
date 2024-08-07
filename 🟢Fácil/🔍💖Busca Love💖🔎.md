
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240806135550.png]]
Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.
![[Pasted image 20240806135949.png]]
Accedo a la dirección encontrada.
![[Pasted image 20240806140024.png]]
Los enlaces no me llevan a ningún otra dirección.
Si inspecciono el código fuente, veo que hay un mensaje comentado.
![[Pasted image 20240806141048.png]]
Se me ocurre probar a utilizar la herramienta de wfuzz para ver si la web es vulnerable a un LFI (Local File Inclusion).
Con el siguiente comando intento adivinar cual es el parámetro que necesito utilizar en caso de que sea vulnerable y que liste por ejemplo el archivo donde se encuentran los usuarios.
```bash
wfuzz --hc 404 --hw 115 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u 172.18.0.2/wordpress/index.php'?'FUZZ=../../../../../../../../../../etc/passwd
```
![[Pasted image 20240806141908.png]]
Ahora con el parámetro love voy a probar a introducir el siguiente contenido en la url de la web.
```bash
http://172.18.0.2/wordpress/index.php?love=../../../../../../../../../../etc/passwd
```
![[Pasted image 20240806142120.png]]Consigo obtener el archivo de la máquina que almacena los usuarios.
Ahora voy a realizar un ataque de fuerza bruta con hydra con los usuarios pedro y rosa.
Para el usuario Pedro no encuentro ninguna contraseña, pero para rosa sí.
![[Pasted image 20240806144351.png]]
Procedo a iniciar sesión por ssh.
![[Pasted image 20240806144413.png]]
Voy a intentar escalar privilegios utilizando algún binario que pueda ejecutar como sudo.
![[Pasted image 20240806144657.png]]
Encuentro un código que parece estar cifrado en hexadecimal.
Voy a descifrarlo con la herramienta online [Rapid Tables](https://www.rapidtables.com/convert/number/hex-to-ascii.html).
![[Pasted image 20240806144922.png]]
Pruebo a intentar iniciar sesión como pedro o como root pero la contraseña parece no ser esa, por lo que igual está cifrada.
Al final parece que está cifrada en Base32.
![[Pasted image 20240806145310.png]]
Inicio sesión como pedro y compruebo los binarios para poder escalar privilegios.
![[Pasted image 20240806145429.png]]
Con la herramienta online [GTFOBins](https://gtfobins.github.io/gtfobins/env/#sudo), introduzco el siguiente comando y consigo ser root.
![[Pasted image 20240806145610.png]]
