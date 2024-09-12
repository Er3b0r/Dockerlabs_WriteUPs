Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240912205450](https://github.com/user-attachments/assets/82b8f091-3f07-4d0d-8ddf-e45d808a180c)

Accedo al recurso web del puerto 80 y me encuentro con una web de un restaurante.

Abajo de la web hay como una especie de formulario para hacer una reserva.

![Pasted image 20240912205625](https://github.com/user-attachments/assets/6fd1daba-997a-4fe6-b931-807f60ee16c6)

Realizo un escaneo de directorios con gobuster pero recibo muchos mensajes de error por lo que decido hacer otra cosa.

Voy a utilizar BurpSuite para mandar una petición del formulario, interceptarla y ver qué pasa.

Configuro el proxy, relleno los datos y mando la petición para recibirla con BurpSuite.

![Pasted image 20240912210635](https://github.com/user-attachments/assets/85558242-033b-4ddd-a421-59b3178d2a33)

Con el Repeater, si envío la petición recibo el siguiente error.

![Pasted image 20240912211118](https://github.com/user-attachments/assets/a5215d31-3afa-4298-81ea-52ff8572abd6)

Buscando el error en el navegador, encuentro que puede ser un error dado porque se puede estar intentando decodear el `userInput` por lo que voy a probar a codificar en base-64 una cadena de caracteres y ver qué me devuelve BurpSuite.

![Pasted image 20240912211858](https://github.com/user-attachments/assets/817c707e-bc52-41e7-a2a1-b322d532182a)


![Pasted image 20240912211922](https://github.com/user-attachments/assets/6017ba6a-f7c2-4899-bd48-38f480bcfb71)

Recibo otro error, por lo que deduzco que estaba en lo correcto y  está intentando decodear el `userInput`.

Voy a intentar listar el `/etc/passwd`.

![Pasted image 20240912212124](https://github.com/user-attachments/assets/ab151198-3fad-4ed3-93fa-c1b141697650)

![Pasted image 20240912212138](https://github.com/user-attachments/assets/4a05dcff-76d3-4f4b-aa0d-aacf2a673171)

Recibo el archivo `/etc/passwd`.

Esto demuestra que puedo inyectar comandos.

![Pasted image 20240912212213](https://github.com/user-attachments/assets/568acd93-9f4b-43ac-9e1b-1fa038a08bf5)

Voy a intentar obtener la contraseña del usuario cachopin con hydra para posteriormente iniciar sesión por ssh.

![Pasted image 20240912212338](https://github.com/user-attachments/assets/3acea571-16f1-4687-9375-a469eb3ca87b)

Una vez inicio como cachopin, encuentro un archivo con varios hashes.

![Pasted image 20240912214016](https://github.com/user-attachments/assets/77766f7f-2014-4cda-bdf3-350712ac5670)

Busco en el navegador alguna herramienta que me ayude pero no encuentro nada por lo que decido ir al GitHub del creador de la máquina [PatxaSec](https://github.com/PatxaSec/SHA_Decrypt) para ver si este tiene alguna herramienta que me ayude.

![Pasted image 20240912214317](https://github.com/user-attachments/assets/b17c8cbd-edf7-411c-b515-89a875e56f07)

Clono la herramienta en mi máquina atacante.

Voy probando cada hash para ver si encuentro alguna password.

Consigo encontrar una password `cecina`.

![Pasted image 20240912214936](https://github.com/user-attachments/assets/a313f692-d9e5-4d93-8e7a-41271a30e861)

Prueba esa contraseña para ser el usuario root.

![Pasted image 20240912215027](https://github.com/user-attachments/assets/6e959188-dd4b-4126-b50c-c342bd4ed2fa)
