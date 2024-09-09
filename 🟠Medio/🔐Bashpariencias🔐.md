Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240909182938](https://github.com/user-attachments/assets/654d5d18-9811-4902-9336-62f9ee75d29e)

Accedo al recuso web  del puerto 80.

![Pasted image 20240909190332](https://github.com/user-attachments/assets/a82b39c1-f21b-49e4-8019-5f6ecd7b4a81)

Obtengo un posible usuario llamado Rosa.

Si ahora voy al apartado de formulario, en la parte de la derecha, puedo ver que en el segundo producto aparece el nombre de rosa.

![Pasted image 20240909190520](https://github.com/user-attachments/assets/18cddf4e-4981-4bfb-aa4e-aa6053b8a01c)

Inspecciono el código fuente de la web y encuentro una posible contraseña para este usuario.

![Pasted image 20240909190553](https://github.com/user-attachments/assets/c51442b7-eca0-416b-86e9-9abc39946350)

Intento acceder con esas credenciales a través de ssh.

![Pasted image 20240909190637](https://github.com/user-attachments/assets/929c9222-a9a6-4cad-9095-f316486c807d)

Investigo un poco y encuentro un directorio `-` con un archivo zip y un txt en su interior.

![Pasted image 20240909191208](https://github.com/user-attachments/assets/67beebde-ef9f-4d4c-a8e1-20b122475f2a)

Me descargo el archivo a mi máquina atacante.

![Pasted image 20240909191524](https://github.com/user-attachments/assets/1422c6b4-9835-49fe-b8a7-3e87844bf4ac)

Utilizo la herramienta John The Ripper para crackear la password del zip y obtener su contenido.

![Pasted image 20240909191838](https://github.com/user-attachments/assets/44ebb0d3-3b5f-42c8-a6f1-49863c3ad03d)

Ahora con esa contraseña inicio sesión como juan.

Una vez que soy juan intento escalar privilegios.

![Pasted image 20240909193015](https://github.com/user-attachments/assets/5dc40c4e-2d98-4100-92fe-28ac3b26495e)

Intento leer el contenido de los archivos.

![Pasted image 20240909193118](https://github.com/user-attachments/assets/14c9df3d-36a2-4b6f-ba96-3582c21878b3)

Inicio sesión como carlos e intento escalar privilegios.

Añado un usuario al archivo `/etc/passwd` para poder iniciar con el sin necesidad de password y con permisos de root.

![Pasted image 20240909194508](https://github.com/user-attachments/assets/22f411b9-6cbe-46d9-a718-ad1832cac7e7)
