Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240901123931](https://github.com/user-attachments/assets/134f4db9-c065-4cef-a41a-56bc4da454c2)

Accedo al recurso web del puerto 80.

![Pasted image 20240901125243](https://github.com/user-attachments/assets/b98463a0-ef0a-4feb-b8cd-a344eeba225a)

Realizo un escaneo de directorios con gobuster.

![Pasted image 20240901125856](https://github.com/user-attachments/assets/9a06a6c9-d284-452c-b8bb-c88c112225f0)

Encuentro la dirección del /robots.txt en la que puedo ver en la parte de abajo un posible usuario admin y una posible password que está hasheada.

![Pasted image 20240902013359](https://github.com/user-attachments/assets/b8b69f3a-3618-40f0-b0e9-41b015976063)

Deshasheo la password.

![Pasted image 20240902013431](https://github.com/user-attachments/assets/730c6512-84b2-42c2-aee3-89b922d95364)

Con estas credenciales inicio sesión en la siguiente web.

![Pasted image 20240902013631](https://github.com/user-attachments/assets/7843921e-a499-4e24-8e87-8c293bced307)

No encuentro nada, pero también puedo iniciar sesión en la dirección /administrator.

![Pasted image 20240902013745](https://github.com/user-attachments/assets/428ed091-7195-4974-9627-7ef95cc7af19)

Ahora voy a tratar de modificar el código de alguna página para intentar inyectar una reverse shell y conseguir ganar acceso desde un terminal.

![Pasted image 20240902014039](https://github.com/user-attachments/assets/924dfd48-0f6c-4405-ae05-cd0358720c50)

![Pasted image 20240902014058](https://github.com/user-attachments/assets/7864c9a7-7f11-46fb-a003-fa789c0643d7)

Pego el código de la reverse shell y guardo los cambios.

![Pasted image 20240902014255](https://github.com/user-attachments/assets/74ce77b6-3b24-47fc-ac53-0464939820ab)

Me pongo en escucha con netcat y luego entro en la siguiente dirección.

![Pasted image 20240902014417](https://github.com/user-attachments/assets/bcee7bea-16ba-4a80-9757-acf7cb5804c4)

Una vez gano acceso hago un tratamiento de la TTY.

```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```

Intento escalar privilegios pero no encuentro la forma.

Si investigo un poco, veo que hay un archivo llamado otro_caramelo.txt en el que encuentro el usuario luisillo y una password luisillosuperpassword.

![Pasted image 20240902015321](https://github.com/user-attachments/assets/e02080b3-0f37-4d24-8fa6-ad307a0d817c)

Intento ser el usuario luisillo.

![Pasted image 20240902020007](https://github.com/user-attachments/assets/dc58eb08-e3e0-4e54-8dc1-058361e98d2c)

Ahora intento escalar a root.

Si hago un `sudo -l` veo que puedo ejecutar el comando /bin/dd como sudo.

Con los siguientes comandos logro escribir en el archivo sudoers que el usuario luisillo pueda ejecutar cualquier comando como cualquier usuario del sistema sin necesidad de introducir una contraseña.

(En la siguiente imagen se ve los permisos de sudo -l ya cambiados por pruebas anteriores durante la resolución de la máquina.)

![Pasted image 20240902020132](https://github.com/user-attachments/assets/faeb6c2d-479a-4515-a32f-d3b30b72139f)
