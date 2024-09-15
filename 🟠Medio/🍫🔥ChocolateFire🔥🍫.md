Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240915195944](https://github.com/user-attachments/assets/f6212fc2-1a1f-4577-b1bf-1e2efcbfa7aa)

Me llama la atención el servicio del puerto 9090, por lo que decido acceder a él a través del navegador.

![Pasted image 20240915200430](https://github.com/user-attachments/assets/99b56250-d836-4dbe-923b-dd8bc0ec2664)

Encuentro un formulario de login.

Pruebo a  acceder indicando credenciales por defecto como ususario:`admin` y password `admin`

![Pasted image 20240915203544](https://github.com/user-attachments/assets/aba69dc6-f7f8-4041-be58-ff74e8f88896)

Si me voy al apartado de `Pulgins` veo que puedo subir un archivo .tar

![Pasted image 20240915204015](https://github.com/user-attachments/assets/1e6111c5-c832-461e-8715-d8bb044af97c)

Voy a tratar de buscar algún exploit para intentar ganar acceso a la máquina.

Con la herramienta searchsploit no encuentro nada.

Si busco en el navegador, encuentro un exploit en un repositorio de [GitHub](https://github.com/miko550/CVE-2023-32315) que me proporciona una consola interactiva con la que puedo ejecutar comandos (RCE).

![Pasted image 20240915204950](https://github.com/user-attachments/assets/8e990173-7ee3-4839-8501-05432bca5ce3)

Me clono el repositorio.

![Pasted image 20240915205143](https://github.com/user-attachments/assets/90384b42-3df0-4180-9a53-b5cfd7899bfe)

Subo el archivo .jar al apartado de plugins.

![Pasted image 20240915205233](https://github.com/user-attachments/assets/aa3b0a49-1850-4ae1-b75d-a20d8f7186bf)

Ahora si voy al apartado de `Server` y `Server Settings`, veo en el menú de la izquierda una opción que se llama `Management Tool`.

![Pasted image 20240915205414](https://github.com/user-attachments/assets/37fbe267-1bc2-4dc3-aaf6-1d08a4cee897)

Me aparece un recuadro en el que ingreso la password que indica el pligin en este caso 123.

Me aparece otra página en la que debo de seleccionar el desplegable e indicar la opción `ststem command`.

![Pasted image 20240915205655](https://github.com/user-attachments/assets/67f7f9e9-e0d1-4d84-98b0-48e42e1bac93)

Me aparece una especie de input en el que si introduzco un comando la máquina lo ejecuta y proyecta su resultado.

![Pasted image 20240915205757](https://github.com/user-attachments/assets/ee3e250a-a991-4f7c-9581-f6ff29599f9f)

Consigo listar el archivo `/etc/passwd` donde se encuentran los usuarios, los apunto e intento hacer fuerza bruta para entrar por ssh.

usuarios --> pinguinacio, chocolatitochingon

Compruebo que tienen un directorio home.

![Pasted image 20240915211554](https://github.com/user-attachments/assets/cd26673a-3098-4272-8c1a-f4ccac8c8f41)

Consigo la password de chocolatitochingon.

![Pasted image 20240915211710](https://github.com/user-attachments/assets/8810638d-cb6c-4cbf-9356-c5e9b7ef2959)

Inicio sesión por ssh.

Intento escalar privilegios.

![Pasted image 20240915212029](https://github.com/user-attachments/assets/1306af87-242b-43c3-a6bd-35e10f523432)

Ejecuto el siguiente comando que me indica en la página [GTFOBins](https://gtfobins.github.io/gtfobins/dpkg/#sudo)

![Pasted image 20240915212100](https://github.com/user-attachments/assets/f2c424c7-a4dd-40f8-9aeb-c1e0abfbbdbd)

Hago un tratamiento de TTY.

```bash
script /dev/null -c bash
```

Soy el usuario pinguinacio.

Intento escalar privilegios.

![Pasted image 20240915213023](https://github.com/user-attachments/assets/6e316612-223a-41bc-972d-f843a8f07047)

Si ejecuto el script, me solicita un imput, en el que yo escribo `a[$(bash >&2)]+42`. Esto me crea una subshell con privileghios de root por lo tanto ya sería root.

![Pasted image 20240915213854](https://github.com/user-attachments/assets/2f42e576-8b1f-4cab-9172-928c373bea6e)
