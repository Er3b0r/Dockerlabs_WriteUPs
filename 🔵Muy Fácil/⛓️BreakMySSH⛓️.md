
___
>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.
![[Pasted image 20240625174454.png]]
>Hay dos maneras de resolver esta máquina, voy a explicar ambas.

---
## Hydra Bruteforce
>Voy a utilizar un ataque de fuerza bruta con hydra al servicio ssh, ya que no tengo ninguna información, probaré con el usuario root a ver si hay suerte y un diccionario de contraseñas.
![[Pasted image 20240625174523.png]]
>Obtengo las credenciales y accedo como root al ssh.
![[Pasted image 20240625174607.png]]

---
## MSFCONSOLE
>Suponiendo que ya he hecho el escaneo con nmap, abro metasploit.
![[Pasted image 20240625213112.png]]
>Busco a ver si hay algún script relacionado con OpenSSH.
>Selecciono el numero 3 ya que me interesa listar los posibles usuarios de ese servicio.
![[Pasted image 20240625213145.png]]
>Configuro el script con los siguientes parámetros, indicando el host de destino, el archivo de diccionario de usuarios que va a utilizar y el puerto si fuese necesario, en este caso no lo es.
>Lanzo el script y ya me reporta varios posibles usuarios.
![[Pasted image 20240625213209.png]]
>Paramos el script ya que he utilizado un diccionario muy extenso y tarda mucho.
>Ahora tenemos unos cuantos usuarios, probamos con root como en el ejemplo anterior utilizando hydra y el mismo diccionario de contraseñas.
>Conseguimos acceso por SSH al usuario root y vamos a listar el archivo **/etc/passwd** para ver si coinciden los usuarios que hemos sacado con el exploit.
![[Pasted image 20240625213452.png]]
>Como podemos apreciar, si que hay usuarios que coinciden y probablemente hubiésemos conseguido obtener el resto pero paramos el exploit por su gran demora de tiempo.
