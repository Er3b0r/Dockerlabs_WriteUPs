Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240811022809](https://github.com/user-attachments/assets/69d5bb32-6b3e-4f7e-8a1a-17930d75a51e)

Accedo al recurso http por el puerto 80.

Encuentro que es una web de una universidad.

Tiene varios apartados.

![Pasted image 20240811023049](https://github.com/user-attachments/assets/f6af4f3c-ab97-4d5e-9a58-7a13c292f897)

De primeras no encuentro nada útil, por lo que voy a realizar fuzzing web con gobuster.

![Pasted image 20240811023733](https://github.com/user-attachments/assets/e1e861fe-5f06-49c8-b441-2433b4574989)

Encuentro varias direcciones, pero la que me parece más interesante es /phpmyadmin.

Encuentro un panel de login.

![Pasted image 20240811030611](https://github.com/user-attachments/assets/3c624c8d-92bc-4fa8-99f5-f4667c03e106)

No encuentro nada, por lo que paso a otra cosa.

Si ahora voy a la web principal al apartado de profesores, encuentro que hay uno que es el administrador de WordPress.

![Pasted image 20240811031416](https://github.com/user-attachments/assets/9d4ac6d2-5cc4-4d5a-bb12-72a24b463abd)

Voy a utilizar la herramienta wpscan para realizar fuerza bruta y ver si puedo obtener alguna credencial a partir del usuario luis como indica el nombre o luisillo como indica su correo.

![Pasted image 20240811040655](https://github.com/user-attachments/assets/27c65b24-dbe3-4c70-a1d2-da8d96f813eb)

Encuentro el usuario luisillo y la contraseña es Luis1981, la contraseña se encuentra en el rockyou.txt, pero también es el año de su nacimiento, por lo que es una contraseña fácil de adivinar.

![Pasted image 20240811040719](https://github.com/user-attachments/assets/7daf5d03-414f-4232-81cb-7fab23375790)

Ahora realizo fuzzing web con gobuster a la dirección /wordpress para ver si tiene algún subdominio.

![Pasted image 20240811040356](https://github.com/user-attachments/assets/d46d8384-df95-4c0f-aaa1-8313f0a10857)

Encuentro el subdominio /wp-admin, pero de primeras no me lo permite.

Debo añadir la ip de la máquina y el nombre del dominio escolares.dl al archivo /etc/hosts.

El nombre del dominio es proporcionado en la url cuando intento acceder al subdominio /wp-admin.

![Pasted image 20240811042021](https://github.com/user-attachments/assets/e9a1c151-6fa3-4c5d-a4cb-bd2fa0393b78)

![Pasted image 20240811042039](https://github.com/user-attachments/assets/510681c6-b856-4c8e-9109-1dfb6a97f14c)

Ahora introduzco las credenciales obtenidas.

Me encuentro lo siguiente, el panel de administrador de wordpress.

![Pasted image 20240811042140](https://github.com/user-attachments/assets/54d6013c-2b56-4593-86dd-8d892dd9466f)

En el menú lateral , hay un apartado que es WP File Manager el cual me va a permitir crear o modificar un archivo.

Puedo utilizar esto para intentar subir una reverse shell.

![Pasted image 20240811042633](https://github.com/user-attachments/assets/a1436813-ac2e-47d2-96d6-9cac6f3fa316)

He utilizado la herramienta online [revshells](https://www.revshells.com/) para crear el código de la reverse shell.

Ahora me pongo en escucha por el puerto indicado en el código con la herramienta netcat.

Busco el archivo reverse.php que acabo de crear.

![Pasted image 20240811043304](https://github.com/user-attachments/assets/6e2bea80-ce9b-4dd2-8c17-aeb2d8230cb2)


![Pasted image 20240811043317](https://github.com/user-attachments/assets/54271277-28e5-4d8e-9f41-a8cb31d695d8)

Ahora hago un tratamiento de la TTY.

```bash
script /dev/null -c bash
Control + Z
stty raw -echo;fg
export TERM=xterm
export SHELL=bash
```

En el direcotrio /home encuentro un archivo llamado secret.txt que parece contener la password de la máquina de luisillo.

![Pasted image 20240811043715](https://github.com/user-attachments/assets/9d2fb59a-8f14-4acf-a9ee-d824020e41ef)

Consigo iniciar sesión como luisillo.

![Pasted image 20240811043852](https://github.com/user-attachments/assets/948bbadc-da63-436f-ba71-03c5c72422e3)

Ahora voy a intentar escalar privilegios con la herramienta online [GTFOBins.](https://gtfobins.github.io/gtfobins/awk/#sudo)

![Pasted image 20240811044424](https://github.com/user-attachments/assets/aa41ae8b-966b-41e5-87da-05d840c33cae)
