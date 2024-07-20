
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240714230141.png]]
![[Pasted image 20240714230431.png]]
>Ahora procedo a realizar fuzzing web en busca de algún posible directorio oculto.
![[Pasted image 20240714230532.png]]
>Encuentro un recurso llamado maintenance.html en el que nos da la ruta a un archivo con una posible contraseña.
![[Pasted image 20240715001328.png]]
>Ahora voy a acceder al servicio ftp con el usuario anonymous.
>Encuentro un archivo y procedo a descargarlo.
![[Pasted image 20240714230625.png]]
>Intento leerlo con john the ripper pero no es posible debido a un error de versión.
![[Pasted image 20240714234020.png]]
>Intento acceder al servicio que se encuentra corriendo el puerto 3000.
>Me encuentro con una página de Grafana.
![[Pasted image 20240714234002.png]]
>Introduzco las credenciales username admin y password admin.
![[Pasted image 20240714234136.png]]
>Cambio la password.
![[Pasted image 20240714234201.png]]
>Consigo acceso al panel como administrador
![[Pasted image 20240714234220.png]]
>Abajo hay un apartado en el que me muestra la versión de Grafana que el sitio web está utilizando.
![[Pasted image 20240715000459.png]]
>Conociendo la versión, procedo a buscar un exploit que me ayude a acceder a la máquina.
![[Pasted image 20240715000657.png]]
>Ejecuto el script y veo que puedo leer archivos.
>Introduzco el archivo que me mostraba la página maintenance.html.
>Obtengo lo que parece ser una password.
>También voy a leer el archivo /etc/passwd para ver los usuarios existentes en el sistema y poder crear un diccionario de usuarios.
![[Pasted image 20240715000904.png]]
>Creo un diccionario de usuarios y con la herramienta hydra, realizo un ataque de fuerza bruta al servicio ssh proporcionando la posible contraseña que acabamos de obtener.
>Obtengo las credenciales del usuario freddy.
![[Pasted image 20240715001152.png]]
>Inicio sesión como freddy en el servicio ssh.
![[Pasted image 20240715001241.png]]
>Compruebo los binarios que puedo ejecutar como sudo.
![[Pasted image 20240715001408.png]]
>Muestro el contenido del archivo.
![[Pasted image 20240715001539.png]]
>Modifico el contenido del archivo para que cuando lo ejecute como sudo, me genere una bash.
>Una vez ejecuto el archivo gano, he logrado escalar privilegios y ser root.
![[Pasted image 20240715002130.png]]
