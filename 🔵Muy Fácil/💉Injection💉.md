>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.

![Pasted image 20240619133509](https://github.com/user-attachments/assets/f9943ee1-1d06-4be3-bda5-f8af37745acc)
>Voy a hacer un poco de fuzzing web para ver si hay algo interesante con la herramienta gobuster.

![Pasted image 20240619133624](https://github.com/user-attachments/assets/944d1461-b793-49a9-a5c3-f5cf01aec53f)
>No he encontrado nada interesante por lo que accedo al index del servicio apache.

![Pasted image 20240619134908](https://github.com/user-attachments/assets/bdfea28e-02e6-4e3d-b32f-31ee54c1ced6)
>Encuentro un formulario de login.
>Voy a probar a hacer un bypass con SQLi.
>	- [Enlace 1 de cheat sheet](https://pentestlab.blog/2012/12/24/sql-injection-authentication-bypass-cheat-sheet/)
>	- [Enlace 2 de cheat sheet](https://book.hacktricks.xyz/pentesting-web/login-bypass/sql-login-bypass)
>	- [Enlace 3 de cheat sheet](https://owasp.org/www-community/attacks/SQL_Injection_Bypassing_WAF)
```sqli
or 1-- -' or 1 or '1"or 1 or"
```
>Y como contraseña indicamos cualquier cosa, por ejemplo 12345.

![Pasted image 20240619135708](https://github.com/user-attachments/assets/0f9f97fc-5171-494e-9c27-192773c647fe)
>Consigo que la página me reporte un usuario y su contraseña.

![Pasted image 20240619135718](https://github.com/user-attachments/assets/0bdf6f78-de4e-4977-b1e0-5f297ce59621)
>Pruebo las credenciales que me ha reportado la web para intentar conectarme a la máquina a través del servicio ssh.

![Pasted image 20240619135839](https://github.com/user-attachments/assets/6d7dad7c-7599-47ce-8cbf-9ace374915bf)
>Consigo acceso y busco el archivo config.php que encontré haciendo fuzzing web con gobuster.
>Listo su contenido y encuentro el usuario root y la posible password paso.

![Pasted image 20240619140129](https://github.com/user-attachments/assets/cdc62eac-7008-4f5f-a0a1-2d8ce5944a50)
>No puedo acceder al usuario root por lo que busco a ver que archivos binarios puedo ejecutar como sudo sin necesidad de password.

![Pasted image 20240619140623](https://github.com/user-attachments/assets/857d8e30-dd2f-4ac5-ac8f-82ba9848375c)
>Veo que puedo ejecutar el binario env.
>Voy a utilizar la herramienta online GTFObins y busco el binario env si puedo ejecutar algún comando para obtener el sudo.
>Lo ejecuto y obtengo una consola sh como root.

![Pasted image 20240619141103](https://github.com/user-attachments/assets/125138fc-93a2-490c-8968-8cb1cc82f53e)

