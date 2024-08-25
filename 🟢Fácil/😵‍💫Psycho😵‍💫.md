Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240824201642](https://github.com/user-attachments/assets/fdc1fb7b-e0fd-4c0a-bc91-fe050fa6e971)

Accedo al recurso web del puerto 80.

![Pasted image 20240824201809](https://github.com/user-attachments/assets/c2cec612-a4d0-4bec-8d07-dffc38a9eaaa)

Realizo una búsqueda de directorios web con gobuster.

![Pasted image 20240824202248](https://github.com/user-attachments/assets/c19ba03a-244d-448c-a83d-70dfd66fb78f)

Accedo al recurso.

![Pasted image 20240824202307](https://github.com/user-attachments/assets/e3b01dfe-177b-43a0-a92f-9d86724cda86)

Encuentro una imagen, intento obtener algún posible dato oculto con herramientas de esteganografía pero no consigo nada.

Ahora voy a intentar hacer fuzzing con wfuzz para ver si es posible que la web sea vulnerable a un ataque LFI (Local File Inclusion) ya que en el pie de index.php aparece un mensaje de [!] ERROR [!] y me hace pensar que puedo introducir algún parámetro.

```bash
wfuzz -c --hc=404 --hw=169 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt http://172.17.0.2/index.php?FUZZ=../../../../../../../../../etc/passwd

```
![Pasted image 20240824203712](https://github.com/user-attachments/assets/c6821ff6-92da-4601-a086-f6f94e9fead4)

Encuentro el parámetro `secret`.

Vuelvo al index.php e introduzco lo siguiente para poder listar el archivo con los usuarios del sistema.

```
http://172.17.0.2/index.php?secret=../../../../../../../../../../etc/passwd
```

![Pasted image 20240824203924](https://github.com/user-attachments/assets/5b1f1a46-c240-4192-9232-64db9a6e9306)

Intento con hydra obtener la contraseña de los usuarios vaxei y luisillo sin suerte.

Voy a probar a obtener la clave id_rsa del usuario vaxei.

![Pasted image 20240824205257](https://github.com/user-attachments/assets/ad456b06-830d-4d95-8546-8f623eaf16d6)

Ahora creo el archivo id_rsa, pego la clave en su interior y le doy permisos al archivo.

![Pasted image 20240824205506](https://github.com/user-attachments/assets/25e75efa-d68a-427e-948b-40e6f0c4fad6)

Intento iniciar sesión al servicio ssh utilizando el archivo id_rsa para hacerme pasar por el usuario vaxei.

![Pasted image 20240824205628](https://github.com/user-attachments/assets/7eb4a349-8b0b-4421-9634-12e20748c324)

Ahora intento escalar privilegios.

Encuentro que puedo ejecutar el binario perl como luisillo, por lo que voy a intentar escalar a ese usuario.

![Pasted image 20240824205939](https://github.com/user-attachments/assets/f6b0cc90-d255-4857-b66f-c34bcaf5ff27)

Intento escalar privilegios para ser root.

![Pasted image 20240824210615](https://github.com/user-attachments/assets/24e8ffd4-2227-4069-9dff-b63fc9629b3a)

Veo que puedo ejecutar python como root sobre el archivo paw.py que se encuentra en el directorio /opt.

Listo el contenido para ver qué es lo que hace el script.

![Pasted image 20240824210636](https://github.com/user-attachments/assets/ffcb8f6f-3cda-4cd0-94fc-b9abeb89f7d8)

A simple vista no veo que haga nada útil por lo que lo intento ejecutar.

![Pasted image 20240824210652](https://github.com/user-attachments/assets/46cf0c3c-6d9d-433a-b435-a3814d229973)

AL ejecutar el script, veo que llama a un archivo llamado subprocess, pero este no existe, por lo que se me ocurre crear un archivo con ese nombre y en su interior cambiar los permisos de la bash para que cualquier usuario pueda ejecutarla como root.

![Pasted image 20240824210912](https://github.com/user-attachments/assets/76e7dc95-57fa-4aa6-a76d-4d2464e2cc36)
