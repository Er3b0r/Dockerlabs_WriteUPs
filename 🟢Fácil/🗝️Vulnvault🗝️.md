Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240828180627.png]]
Voy al recurso web del puerto 80.
![[Pasted image 20240828180639.png]]
Realizo un escaneo de directorios con gobuster.
![[Pasted image 20240828181128.png]]
En la siguiente dirección puedo subir un archivo, por lo que voy a intentar subir un archivo php con una reverse shell.
![[Pasted image 20240828181920.png]]
Subo el archivo pero no se muestra en la página upload.php ni en ninguna que haya encontrado.
Voy a probar a ver si en la dirección /old puedo inyectar comandos en los campos para generar un reporte.
Compruebo que la sanitización de los campos está mal realizada y descubro que puedo ejecutar comandos añadiendo el símbolo ; seguido del comando.
![[Pasted image 20240828185048.png]]
Voy a intentar listar el archivo de los usuarios de la máquina.
![[Pasted image 20240828185212.png]]
Encuentro el usuario samara, por lo que voy a intentar acceder a la máquina mediante ssh.
Intento ahora listar el id_rsa introduciendo:
```bash
; cat /home/samara/.ssh/id_rsa
```
Copio la clave desde el código fuente, creo un archivo llamado id_rsa, le asigno permisos 600 y pego la clave ahí.
![[Pasted image 20240828185641.png]]
Accedo a través de ssh con el archivo con la clave.
![[Pasted image 20240828185910.png]]
Intento escalar privilegios pero de primeras no encuentro nada a simple vista.
Si investigo un poco, encuentro un archivo sh que escribe un string en el archivo /home/samara/message.txt.
Si compruebo en contenido del archivo, veo que el contenido se corresponde, por lo que intuyo que hay algún proceso oculto que ejecuta ese script.
![[Pasted image 20240828193400.png]]
Intento editar el contenido para cambiar los permisos de la bash y poder ejecutarla y poder escalar privilegios.
![[Pasted image 20240828194241.png]]
![[Pasted image 20240828194253.png]]

Flag samara --> 030208509edea7480a10b84baca3df3e
Flag root --> 640c89bbfa2f70a4038fd570c65d6dcc
