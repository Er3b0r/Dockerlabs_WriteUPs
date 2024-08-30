Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240827173544](https://github.com/user-attachments/assets/3e1f111c-233c-4fdd-a383-a54af3abff73)

Voy al recurso web del puerto 80.

![Pasted image 20240827173623](https://github.com/user-attachments/assets/177991b0-b23b-4fdb-bb96-ef0385d45e26)

Hago un escaneo de directorios con gobuster.

![Pasted image 20240827174211](https://github.com/user-attachments/assets/0cb25ab6-1276-49cd-9db7-6b516aeafb55)

Obtengo los siguientes recursos.

Una página donde a través de una API consulta el tiempo de una cuidad.

![Pasted image 20240827174235](https://github.com/user-attachments/assets/6963dac6-fd72-4d38-b8ef-e0b7ce930aac)

Una página de error de login.

![Pasted image 20240827174349](https://github.com/user-attachments/assets/47238cf8-4f1b-4006-9da0-adff1387e16e)

Voy a intentar conseguir el usuario y la password para iniciar sesión con sqlmap apuntando al index.php.

![Pasted image 20240827175654](https://github.com/user-attachments/assets/cf588339-f0f3-4746-9eba-c4fbde74c2fa)

Encuentro las siguientes bases de datos.

![Pasted image 20240827175724](https://github.com/user-attachments/assets/ca920664-a933-4559-9913-1096e3c1d6ff)

Ahora me interesa saber el contenido de la base de datos de users.

![Pasted image 20240827175917](https://github.com/user-attachments/assets/15d026ab-4798-405f-8f33-5eb09b5bd2b9)

Encuentro la tabla usuarios.

![Pasted image 20240827175933](https://github.com/user-attachments/assets/ad2cd394-9ee4-47fa-a5e2-8008a35c1462)

Quiero saber el contenido de esa tabla.

![Pasted image 20240827180031](https://github.com/user-attachments/assets/cbfaf72f-5071-4886-977d-0cd65d910e76)

Encuentro estas columnas.

![Pasted image 20240827180106](https://github.com/user-attachments/assets/181f9a5a-ca6d-43e6-9289-713a718b9474)

Listo el contenido la cada columna de la siguiente manera.

![Pasted image 20240827180256](https://github.com/user-attachments/assets/1e0720fe-771b-4ad6-af75-ac9e28bd135d)

Obtengo el siguiente resultado.

![Pasted image 20240827180318](https://github.com/user-attachments/assets/1c23bec1-fcc3-44e8-ac1f-6dbac893be81)

Ahora con los usuarios y sus contraseñas, intento iniciar sesión en el panel de login.

Si inicio sesión con cualquier usuario, me lleva a la dirección de page.php donde puedo consultar el clima de una ciudad.

El usuario con id 4 de la base de datos puede sugerir que podría haber un directorio oculto que no he logrado ver con el escaneo de directorios, por lo que voy a probar a buscarlo de manera manual introduciendo después de la dirección ip, el nombre del usuario directorio y si no encuentro nada, pruebo con el nombre de la contraseña.

Encuentro el siguiente recurso con una imagen.

![Pasted image 20240827181801](https://github.com/user-attachments/assets/4cb55a46-ba55-4041-b239-c0cc10dcd366)

Descargo la imagen para ver si con herramientas de esteganografía puedo obtener algo.

Con la herramienta steghide intento extraer posible información oculta.

![Pasted image 20240827182548](https://github.com/user-attachments/assets/e4f7d991-fbe4-456d-972d-c9e00008c118)

Veo que tiene una contraseña, por lo que voy a intentar crackearla con la herramienta stegcracker.

Obtengo la posible contraseña.

![Pasted image 20240827182914](https://github.com/user-attachments/assets/69208c51-e100-485f-893a-8c37bbde6836)

Vuelvo a utilizar la herramienta steghide.

Obtengo un archivo llamado ocultito.zip.

![Pasted image 20240827183035](https://github.com/user-attachments/assets/4457052b-e1bf-4ab9-97cd-303f37c7dc22)

Intento descomprimirlo pero también tiene contraseña por lo que voy a usar john the ripper para crackerarla.

![Pasted image 20240827183142](https://github.com/user-attachments/assets/b1f44759-cb6f-49eb-b660-9f5eedb23fd4)

Obtengo el contenido oculto de la siguiente manera.

![Pasted image 20240827183538](https://github.com/user-attachments/assets/ae3cb02d-8189-48c7-b9ff-27b17bcee273)

Con el usuario y la contraseña voy a intentar iniciar sesión por ssh.

![Pasted image 20240827183637](https://github.com/user-attachments/assets/9d0684b5-9fbc-4745-ac22-8665b47a9fef)

Ahora intento escalar privilegios buscando los permisos SUID.

![Pasted image 20240827183836](https://github.com/user-attachments/assets/6c6a3069-1d95-43d9-857d-b343afce280b)

Consigo ser root gracias al binario find.

![Pasted image 20240827184041](https://github.com/user-attachments/assets/3bfc034f-51e1-4567-a87e-c9bf5fafe4e5)
