Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240805005020](https://github.com/user-attachments/assets/6b27b20c-1db1-48b2-8f31-e68e3d0696ff)

En el recurso web del puerto 80, encuentro un apartado llamado `Acceder al Backend` en el que parece ser que se ven archivos subidos. El recurso web al que he accedido se llama upload.

Puedo utilizar este recurso más adelante para ejecutar un script y que me proporcione una reverse shell.

Por ahora voy a acceder al servicio ftp.

![Pasted image 20240805005708](https://github.com/user-attachments/assets/447b3f49-af59-4b11-a4f0-4a70e414f1b5)

Veo que tengo todos los permisos sobre el directorio upload, probablemente sea el mismo recurso que he encontrado en la web.

Voy a tratar de subir un script php que me proporcione una reverse shell.

Para ello voy a utilizar la herramienta online [revshells](https://www.revshells.com/).

Tengo que asignarle todos los permisos o por lo menos de ejecución al script.php.

![Pasted image 20240805010117](https://github.com/user-attachments/assets/7ae1fc4b-b71b-4bb6-9dcf-1e315b1d237a)

Ahora me pongo en escucha con netcat por el puerto indicado.

![Pasted image 20240805010212](https://github.com/user-attachments/assets/589b836a-033d-43b2-a1f7-9196e16ff05e)

Subo el archivo al directorio upload del servicio ftp.

![Pasted image 20240805010302](https://github.com/user-attachments/assets/1d0a37ad-eec7-486a-bded-8973cef9ebdb)

Voy al recurso web upload y ejecuto el script.php para poder recibir una reverse shell.

![Pasted image 20240805010335](https://github.com/user-attachments/assets/8f218d53-bfd3-4fb6-a25f-4e14aa1b6358)

Selecciono el archivo `script.php` y gano acceso a la máquina en el terminal donde estaba escuchando con netcat.

Ahora hago un tratamiento de la TTY.

```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```

Intento escalar privilegios para ser el usuario `pingu`.

![Pasted image 20240926235533](https://github.com/user-attachments/assets/e1cac712-8dc9-4413-9ded-efed77fde6b4)

Intento escalar privilegios para ser el usuario `gladys`.

![Pasted image 20240926235825](https://github.com/user-attachments/assets/9e6aa8f9-0d37-4cd1-8489-c3f82830cf93)

Intento escalar privilegios para ser el usuario `root`.

![Pasted image 20240927000955](https://github.com/user-attachments/assets/0cfdf5cf-938b-48c9-8f40-00aaa0e9d499)

Ahora como no puedo editar el archivo voy a añadir directamente un usuario nuevo con una password y privilegios de root.

```bash
openssl passwd password
echo 'hacker:$1$OM6nPqQf$9TzDN//UqkfWpAZY7lZhL1:0:0::/home/hacker:/bin/bash
' >> /etc/passwd
```

Ahora inicio sesión como el usuario que acabo de añadir y ya sería root.

![Pasted image 20240927002029](https://github.com/user-attachments/assets/91f10958-45f4-44b9-aa7d-2615adc0290b)
