Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20241001012916](https://github.com/user-attachments/assets/bdbaf76f-e16c-4ce1-8ac3-376c4d9c5a99)

Accedo al recurso web del puerto 80.

![Pasted image 20241001012936](https://github.com/user-attachments/assets/61aa35bd-f14c-40ed-8934-2f75c0108b0a)

De primeras no encuentro nada, por lo que voy a realizar un escaneo de directorios con `gobuster`.

![Pasted image 20241001014112](https://github.com/user-attachments/assets/d85a19b8-1855-4d32-92f9-ef564c733980)

Tampoco encuentro ningún directorio oculto.

Leyendo de nuevo la `Pista`, voy a interpretar que `A` es un usuario, por lo que voy a realizar fuerza bruta a ssh para ver si consigo acceso.

![Pasted image 20241001014432](https://github.com/user-attachments/assets/46ea73ba-52cd-44b7-a877-af1b9ecaad55)

Pruebo las credenciales y gano acceso a la máquina.

![Pasted image 20241001014528](https://github.com/user-attachments/assets/ecbe9bfa-4cf4-4ee7-9105-4258871de7a3)

En la ruta `/srv/ftp` encuentro varios archivos.

Si muestro el contenido de `hash_scpencer.txt` veo que contiene una cadena de caracteres cifrada en lo que puede ser MD5.

![Pasted image 20241001015424](https://github.com/user-attachments/assets/b7928fd1-b4e9-4fd3-8d79-86c0564fc5f5)

Compruebo si puedo descifrarlo con una herramienta online.

![Pasted image 20241001015454](https://github.com/user-attachments/assets/b98a8362-4506-4531-8169-e556b7259ad2)

Si ahora muestro el contenido de `pista_fuerza_bruta.txt` me dice que pruebe a realizar un ataque de fuerza bruta al usuario `spencer`.

![Pasted image 20241001015547](https://github.com/user-attachments/assets/af61870b-062d-4aa4-b06a-360b9d34725f)

![Pasted image 20241001015559](https://github.com/user-attachments/assets/42d09dad-c62b-4d7f-a62d-386058dbd8e1)

Veo que ambas contraseñas coinciden por lo que me imagino que el resto de archivos son pequeños retos para poder descifrar la contraseña de diferentes formas.

Voy a iniciar como el usuario `spencer`.

![Pasted image 20241001015715](https://github.com/user-attachments/assets/47e9829f-b020-449f-86ec-1b60aa346906)

Ahora voy a intentar escalar privilegios.

![Pasted image 20241001015831](https://github.com/user-attachments/assets/c449ec34-9f6a-4e76-9df5-f0b4e89a1b6c)
