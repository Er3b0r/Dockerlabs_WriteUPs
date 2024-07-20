>Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240714230141](https://github.com/user-attachments/assets/ee386ace-8e08-4355-a18c-0a0a3c66bb52)
![Pasted image 20240714230431](https://github.com/user-attachments/assets/352d49df-c108-46e7-b395-77073a0e749b)
>Ahora procedo a realizar fuzzing web en busca de algún posible directorio oculto.

![Pasted image 20240714230431](https://github.com/user-attachments/assets/036bcbef-47a0-439a-b2d8-e61564783e61)
>Encuentro un recurso llamado maintenance.html en el que nos da la ruta a un archivo con una posible contraseña.

![Pasted image 20240715001328](https://github.com/user-attachments/assets/23079130-ec2f-43fe-abaf-9214401c27d5)
>Ahora voy a acceder al servicio ftp con el usuario anonymous.
>Encuentro un archivo y procedo a descargarlo.

![Pasted image 20240714230625](https://github.com/user-attachments/assets/18e0afbc-31fc-4864-9614-5f024155f641)
>Intento leerlo con john the ripper pero no es posible debido a un error de versión.

![Pasted image 20240714234020](https://github.com/user-attachments/assets/30a53dd0-6bb2-4a25-898b-02015ca30cb7)
>Intento acceder al servicio que se encuentra corriendo el puerto 3000.
>Me encuentro con una página de Grafana.

![Pasted image 20240714234002](https://github.com/user-attachments/assets/5e004317-2ccc-442e-a831-52ca77076a52)
>Introduzco las credenciales username admin y password admin.

![Pasted image 20240714234136](https://github.com/user-attachments/assets/5e54ff90-22e0-4a86-9d78-70285c2dc63e)
>Cambio la password.

![Pasted image 20240714234201](https://github.com/user-attachments/assets/6602b1dc-b25e-42ce-891e-ad754c182cbb)
>Consigo acceso al panel como administrador

![Pasted image 20240714234220](https://github.com/user-attachments/assets/dd5a2f4e-fc50-406f-9739-3210071668f4)
>Abajo hay un apartado en el que me muestra la versión de Grafana que el sitio web está utilizando.

![Pasted image 20240715000459](https://github.com/user-attachments/assets/1a475c59-eec9-49b1-900d-5411fa89ef1d)
>Conociendo la versión, procedo a buscar un exploit que me ayude a acceder a la máquina.

![Pasted image 20240715000657](https://github.com/user-attachments/assets/9929d6d6-55ab-4d28-bc48-3cd03c061c67)
>Ejecuto el script y veo que puedo leer archivos.
>Introduzco el archivo que me mostraba la página maintenance.html.
>Obtengo lo que parece ser una password.
>También voy a leer el archivo /etc/passwd para ver los usuarios existentes en el sistema y poder crear un diccionario de usuarios.

![Pasted image 20240715000904](https://github.com/user-attachments/assets/529b2a54-bb36-4540-ace4-7915d4c8139d)
>Creo un diccionario de usuarios y con la herramienta hydra, realizo un ataque de fuerza bruta al servicio ssh proporcionando la posible contraseña que acabamos de obtener.
>Obtengo las credenciales del usuario freddy.

![Pasted image 20240715001152](https://github.com/user-attachments/assets/f6dc8d0c-626e-4555-b59d-878755fb475d)
>Inicio sesión como freddy en el servicio ssh.

![Pasted image 20240715001241](https://github.com/user-attachments/assets/3907c743-08bf-4b7d-95f1-6067fc0f9780)
>Compruebo los binarios que puedo ejecutar como sudo.

![Pasted image 20240715001408](https://github.com/user-attachments/assets/c37d1081-58e2-429f-84f8-86d4fc10cfa1)
>Muestro el contenido del archivo.

![Pasted image 20240715001539](https://github.com/user-attachments/assets/f9d9b8af-0604-4828-969c-412c49f1596f)
>Modifico el contenido del archivo para que cuando lo ejecute como sudo, me genere una bash.
>Una vez ejecuto el archivo gano, he logrado escalar privilegios y ser root.

![Pasted image 20240715002130](https://github.com/user-attachments/assets/628923e0-3d2b-4fea-82a9-89ba9e3cbd2b)
