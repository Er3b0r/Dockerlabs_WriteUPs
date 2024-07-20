
---
>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.
![[Pasted image 20240619133509.png]]
>Voy a hacer un poco de fuzzing web para ver si hay algo interesante con la herramienta gobuster.
![[Pasted image 20240619133624.png]]
>No he encontrado nada interesante por lo que accedo al index del servicio apache.
![[Pasted image 20240619134908.png]]
>Encuentro un formulario de login.
>Voy a probar a hacer un bypass con SQLi.
>	- [Enlace 1 de cheat sheet](https://pentestlab.blog/2012/12/24/sql-injection-authentication-bypass-cheat-sheet/)
>	- [Enlace 2 de cheat sheet](https://book.hacktricks.xyz/pentesting-web/login-bypass/sql-login-bypass)
>	- [Enlace 3 de cheat sheet](https://owasp.org/www-community/attacks/SQL_Injection_Bypassing_WAF)
```sqli
or 1-- -' or 1 or '1"or 1 or"
```
>Y como contraseña indicamos cualquier cosa, por ejemplo 12345.
![[Pasted image 20240619135708.png]]
>Consigo que la página me reporte un usuario y su contraseña.
![[Pasted image 20240619135718.png]]
>Pruebo las credenciales que me ha reportado la web para intentar conectarme a la máquina a través del servicio ssh.
![[Pasted image 20240619135839.png]]
>Consigo acceso y busco el archivo config.php que encontré haciendo fuzzing web con gobuster.
>Listo su contenido y encuentro el usuario root y la posible password paso.
![[Pasted image 20240619140129.png]]
>No puedo acceder al usuario root por lo que busco a ver que archivos binarios puedo ejecutar como sudo sin necesidad de password.
![[Pasted image 20240619140623.png]]
>Veo que puedo ejecutar el binario env.
>Voy a utilizar la herramienta online GTFObins y busco el binario env si puedo ejecutar algún comando para obtener el sudo.
>Lo ejecuto y obtengo una consola sh como root.
>![[Pasted image 20240619141103.png]]
