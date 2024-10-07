Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20241007012850](https://github.com/user-attachments/assets/93037ab5-3c64-4f1b-b228-b92cd82a38c6)

Accedo al recurso web del puerto 80.

![Pasted image 20241007013029](https://github.com/user-attachments/assets/4f6a54d9-37d7-4bbf-93cd-28c98fa16099)

Encuentro una web en la que puedo buscar algún producto pero la petición la envía a otra IP distinta la `20.20.20.3/process.php` por el método POST.

![Pasted image 20241007013040](https://github.com/user-attachments/assets/c8ebd60b-f21f-4882-a7c7-0c11c0aefb9a)

Realizo un escaneo de directorios con gobuster.

![Pasted image 20241007014140](https://github.com/user-attachments/assets/46011ae4-f93d-4464-bb26-a6cd83f512ab)

En la ruta `/info` encuentro lo siguiente.

![Pasted image 20241007014209](https://github.com/user-attachments/assets/4ade3086-bfb5-4895-81a1-7e5a5bb1a181)

Encuentro un posible usuario `Toni`, por lo que voy a intentar realizar fuerza bruta a la máquina utilizando hydra.

![Pasted image 20241007014428](https://github.com/user-attachments/assets/33e499fa-3270-46a7-b735-fb69691f3f32)

Con las credenciales obtenidas intento acceder a la máquina.

![Pasted image 20241007014513](https://github.com/user-attachments/assets/8ec6dcd7-a16a-4982-bf31-05cf8d64ab78)

Volviendo un poco atrás y viendo de nuevo el código fuente del recurso web, veo que hay una "segunda máquina" a la que va la petición.

![Pasted image 20241007014956](https://github.com/user-attachments/assets/e3a157a2-c2d0-4ca6-8d50-1b536c5fd72d)

Compruebo que desde la máquina víctima, en teoría tengo acceso.

En el código fuente veo también que hay un campo llamado `CMD`, voy a intentar inyectar código mandando una petición con `curl` por `POST`.

![Pasted image 20241007015524](https://github.com/user-attachments/assets/538180c2-7962-468e-83bc-9a9df58f7bec)

Funciona pero no puedo concatenar comandos.

Voy a intentar enviarme una reverse shell a otro terminal que se encuentre escuchando con netcat.

![Pasted image 20241007015936](https://github.com/user-attachments/assets/f55fc646-52de-4758-93f1-bd3cd8d14871)
![Pasted image 20241007015954](https://github.com/user-attachments/assets/bc06944b-a166-485a-a242-23b7b36a181e)
![Pasted image 20241007020006](https://github.com/user-attachments/assets/1208298e-e910-4894-8747-37bb4ea0c3cf)

Hago un tratamiento de TTY.

```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```

Intento escalar privilegios y veo que tengo permisos SUID sobre el binario curl.

![Pasted image 20241007020351](https://github.com/user-attachments/assets/41f83a9b-8590-476c-b07d-c42f5a4bb500)

Voy a intentar modificar el archivo `/etc/passwd` con el comando curl.

Para ello primero debo de copiar el contenido en otro archivo, quitar la primera x el usuario `root` para poder iniciar como dicho usuario sin necesidad de introducir una password.

![Pasted image 20241007021303](https://github.com/user-attachments/assets/806e9f64-b992-419d-a57b-254d33b672e2)

Y por último debo de sustituir el archivo `/etc/passwd` original por el nuevo archivo modificado.

![Pasted image 20241007021422](https://github.com/user-attachments/assets/18803a87-7127-4a92-b996-fb35c47d1ed4)
