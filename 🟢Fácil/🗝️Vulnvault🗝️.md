Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240828180627](https://github.com/user-attachments/assets/cabd4e52-d7fa-4c25-83b8-b16195940aa5)

Voy al recurso web del puerto 80.

![Pasted image 20240828180639](https://github.com/user-attachments/assets/7b5bbf25-b89d-4f26-9ed5-7e2ced445167)

Realizo un escaneo de directorios con gobuster.

![Pasted image 20240828181128](https://github.com/user-attachments/assets/0663ea56-dfb7-49f9-90b1-202993248a10)

En la siguiente dirección puedo subir un archivo, por lo que voy a intentar subir un archivo php con una reverse shell.

![Pasted image 20240828181920](https://github.com/user-attachments/assets/545e2dc0-25e6-478b-9bfe-6d7748fb75c1)

Subo el archivo pero no se muestra en la página upload.php ni en ninguna que haya encontrado.

Voy a probar a ver si en la dirección /old puedo inyectar comandos en los campos para generar un reporte.

Compruebo que la sanitización de los campos está mal realizada y descubro que puedo ejecutar comandos añadiendo el símbolo ; seguido del comando.

![Pasted image 20240828185048](https://github.com/user-attachments/assets/0d7c643c-5cd7-4c2c-93ab-3e293b6ca804)

Voy a intentar listar el archivo de los usuarios de la máquina.

![Pasted image 20240828185212](https://github.com/user-attachments/assets/46860e37-73fe-480e-b235-452acbd1d3a2)

Encuentro el usuario samara, por lo que voy a intentar acceder a la máquina mediante ssh.

Intento ahora listar el id_rsa introduciendo:

```bash
; cat /home/samara/.ssh/id_rsa
```

Copio la clave desde el código fuente, creo un archivo llamado id_rsa, le asigno permisos 600 y pego la clave ahí.

![Pasted image 20240828185641](https://github.com/user-attachments/assets/4f359a25-6f4a-484e-aa35-3ef93a6b1d82)

Accedo a través de ssh con el archivo con la clave.

![Pasted image 20240828185910](https://github.com/user-attachments/assets/77bc7789-9d4e-4664-933d-5709191c831a)

Intento escalar privilegios pero de primeras no encuentro nada a simple vista.

Si investigo un poco, encuentro un archivo sh que escribe un string en el archivo /home/samara/message.txt.

Si compruebo en contenido del archivo, veo que el contenido se corresponde, por lo que intuyo que hay algún proceso oculto que ejecuta ese script.

![Pasted image 20240828193400](https://github.com/user-attachments/assets/c6a14e50-cd7c-45d3-b595-119ea06823f7)

Intento editar el contenido para cambiar los permisos de la bash y poder ejecutarla y poder escalar privilegios.

![Pasted image 20240828194241](https://github.com/user-attachments/assets/64772bec-e6df-47ee-891b-228c26eca47c)

![Pasted image 20240828194253](https://github.com/user-attachments/assets/df6da613-2305-4935-8338-9bfa8262f205)


Flag samara --> 030208509edea7480a10b84baca3df3e

Flag root --> 640c89bbfa2f70a4038fd570c65d6dcc
