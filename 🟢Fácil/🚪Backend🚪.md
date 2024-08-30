Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240830183501](https://github.com/user-attachments/assets/5e4dfd13-c443-4c5c-96fe-23615bd35b49)

Realizo un escaneo de directorios con gobuster.

![Pasted image 20240830184321](https://github.com/user-attachments/assets/d0bbfe8b-eaaa-403d-b3db-a5050ec78f65)

Encuentro una página de login.

![Pasted image 20240830184514](https://github.com/user-attachments/assets/51403908-f8c3-4486-a57a-2dbbc5bf0ac2)

Voy a utilizar la herramienta sqlmap para intentar descubrir los datos de la base de datos de la web.

![Pasted image 20240830184815](https://github.com/user-attachments/assets/a3017e34-9a6e-4ab7-acfb-27fc7980c24d)

Encuentro las siguientes bases de datos.

![Pasted image 20240830184837](https://github.com/user-attachments/assets/ca7334c6-5646-4995-8b79-cfaf2139307a)

Ahora me interesa saber el contenido de la base de datos de users.

![Pasted image 20240830185023](https://github.com/user-attachments/assets/2907a287-dfaf-4466-aaa7-1debd8cf74b8)

Encuentro la tabla usuarios.

![Pasted image 20240830185042](https://github.com/user-attachments/assets/feed78ef-d6fa-4ec5-96fc-68a5f21ba3f2)

Quiero saber el contenido de esa tabla.

![Pasted image 20240830185139](https://github.com/user-attachments/assets/3130abea-8c95-4b2e-bc02-7d3b481cd955)

Encuentro estas columnas.

![Pasted image 20240830185216](https://github.com/user-attachments/assets/05c9cc87-9378-4db1-bee3-92867b4d1e4f)

Listo el contenido la cada columna de la siguiente manera.

![Pasted image 20240830185323](https://github.com/user-attachments/assets/80e026d7-727e-46e3-9656-f3a39f7d5160)

Obtengo el siguiente resultado.

![Pasted image 20240830185446](https://github.com/user-attachments/assets/180ff387-7c71-47f6-bf20-7ffe2c331cf5)

Utilizo el usuario pepe y su password para iniciar sesión en la máquina a través del ssh.

Intento escalar privilegios.

Utilizo el binario grep para leer la contraseña haseada de root.

![Pasted image 20240830192033](https://github.com/user-attachments/assets/bcb6569b-9f0d-4372-9553-75ef7dde8999)

El hash es un md5. [(MD5 Decrypt)](https://www.md5online.org/md5-decrypt.html#google_vignette)

![Pasted image 20240830192333](https://github.com/user-attachments/assets/9a3d40d5-8e74-4e44-841c-9e0ed230e294)

Inicio sesión como root.

![Pasted image 20240830192433](https://github.com/user-attachments/assets/eb515c92-158b-458b-9a7c-d0106c927424)
