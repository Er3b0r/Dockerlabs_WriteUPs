
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240909182938.png]]
Accedo al recuso web  del puerto 80.
![[Pasted image 20240909190332.png]]
Obtengo un posible usuario llamado Rosa.
Si ahora voy al apartado de formulario, en la parte de la derecha, puedo ver que en el segundo producto aparece el nombre de rosa.
![[Pasted image 20240909190520.png]]
Inspecciono el código fuente de la web y encuentro una posible contraseña para este usuario.
![[Pasted image 20240909190553.png]]
Intento acceder con esas credenciales a través de ssh.
![[Pasted image 20240909190637.png]]
Investigo un poco y encuentro un directorio `-` con un archivo zip y un txt en su interior.
![[Pasted image 20240909191208.png]]
Me descargo el archivo a mi máquina atacante.
![[Pasted image 20240909191524.png]]
Utilizo la herramienta John The Ripper para crackear la password del zip y obtener su contenido.
![[Pasted image 20240909191838.png]]
Ahora con esa contraseña inicio sesión como juan.
Una vez que soy juan intento escalar privilegios.
![[Pasted image 20240909193015.png]]
Intento leer el contenido de los archivos.
![[Pasted image 20240909193118.png]]
Inicio sesión como carlos e intento escalar privilegios.
Añado un usuario al archivo `/etc/passwd` para poder iniciar con el sin necesidad de password y con permisos de root.
![[Pasted image 20240909194508.png]]
