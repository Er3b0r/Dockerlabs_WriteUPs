Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240831132625](https://github.com/user-attachments/assets/169cbec5-cc34-498b-8713-b8c3129b00e6)

Realizo un escaneo de directorios con gobuster.

![Pasted image 20240831133313](https://github.com/user-attachments/assets/6ad451d0-9d10-4575-889c-4020c6a87746)

Veo el código fuente del recurso web del puerto 80 y descubro un dominio al que no puedo acceder, por lo que lo añado al /etc/hosts.

![Pasted image 20240831132724](https://github.com/user-attachments/assets/e6f0db24-3d93-4ccb-b2f8-51dc58fc4a9b)

Ahora ya puedo acceder.

![Pasted image 20240831132822](https://github.com/user-attachments/assets/bb9cd7d1-6d56-40c6-ad94-2048ece152a6)

Si ahora realizo un escaneo de directorios de este dominio, encuentro las siguientes direcciones y puedo ver que se trata de un WordPress.

![Pasted image 20240831133925](https://github.com/user-attachments/assets/5b93f70e-b326-43f9-8d7f-4df1ac42800f)

En la web principal de pressenter.hl, arriba a la derecha hay un apartado "Las aventuras de pressi y su fiel hacker" en el que si accedo me lleva a un post.

![Pasted image 20240831140010](https://github.com/user-attachments/assets/d0e83fb4-f8d2-42c1-8eeb-8df2149cfce3)

Veo que pueden existir dos posibles usuarios, pressi y Echo.

Voy a intentar acceder como pressi al WordPress.

![Pasted image 20240831140429](https://github.com/user-attachments/assets/7f5da1fd-d01e-47dd-a9e2-bbccd046f7fd)

Veo que el usuario es correcto pero la password no.

Con la herramienta wpscan, voy a intentar realizar fuerza bruta para intentar obtener la password del usuario pressi.

![Pasted image 20240831141224](https://github.com/user-attachments/assets/660147d8-c608-4f64-a768-27d50fb1f3a3)

Encuentro las siguientes credenciales.

![Pasted image 20240831141242](https://github.com/user-attachments/assets/04b2d68a-9c30-491c-8016-0e6bc00a8bcb)

Consigo iniciar sesión en WordPress.

![Pasted image 20240831141321](https://github.com/user-attachments/assets/ac9038aa-3f49-4357-87b7-ace2c91eb397)

Voy a herramientas, editor de archivos de temas, selecciono el tema a editar Twenty Twenty-Two, modifico el archivo index.php y pego el codigo para obtener una reverse shell.

![Pasted image 20240831154747](https://github.com/user-attachments/assets/861eb023-1ad8-4fa6-9d86-f9c8c2df8ff9)

Me pongo en escucha con netcat desde el terminal.

Voy a la siguiente URL para obtener la reverse shell.

```
http://pressenter.hl/wp-content/themes/twentytwentytwo/index.php
```

![Pasted image 20240831154530](https://github.com/user-attachments/assets/a2365544-be26-4909-948d-22a762e0b2d1)

Hago el respectivo tratamiento de TTY.

```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```

Encuentro un archivo en /tmp que no puedo leer si no soy el usuario mysql y tambien encuentro el directorio /home/enter pero no puedo entrar si no soy el usuario enter.

Accedo al recurso /var/www/pressenter/wp-config.php.

![Pasted image 20240831165633](https://github.com/user-attachments/assets/44356d4f-d8ab-4908-80b1-7e1fa0d67271)

Encuentro una base de datos con un user y una password.

Entro en la base de datos con esas credenciales.

Busco en wp_usernames y encuentro los datos del usuario enter.

![Pasted image 20240831165755](https://github.com/user-attachments/assets/ec4a43c6-3b86-4e24-a374-f155a4685f30)

Inicio sesión como el usuario enter y encuentro su flag.

![Pasted image 20240831165901](https://github.com/user-attachments/assets/f715169e-5eec-45a7-812a-c7543150ed51)

Ahora voy a intentar escalar privilegios y ser root.

No consigo nada más que leer un archivo llamado root.txt pero no es útil.

Si intento acceder a root utilizando la password del usuario enter consigo acceso y puedo ver la flag.

![Pasted image 20240902000359](https://github.com/user-attachments/assets/4ff33cbc-bfa8-4718-8629-204a6c37b744)

# 🏴‍☠️Flags🏴‍☠️

Flag enter --> 4a05a7bc45edb56b1f033ca1606e176c

Flag root --> 4e4a603de810988e0842777de1d97e68
