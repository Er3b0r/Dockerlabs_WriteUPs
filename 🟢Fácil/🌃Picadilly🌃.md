>Escaneo de puertos y servicios utilizando nmap.

![Pasted image 20240722220922](https://github.com/user-attachments/assets/3152f899-8fc9-4f25-83d0-feae4034b780)
>Voy al navegador y voy a la dirección 172.17.0.2:80.

![Pasted image 20240722221119](https://github.com/user-attachments/assets/80460f35-c4fc-4156-be18-323a187f051c)
>El contenido del archivo backup.txt es el siguiente.

![Pasted image 20240722221149](https://github.com/user-attachments/assets/071b203b-43d8-46b4-b802-f9b16ee87255)
>Me dice que el usuario es mateo y la contraseña esta cifrada posiblemente con el cifrado César.
>Voy a utilizar una herramienta online para obtener el posible descrifrado.

![Pasted image 20240722221809](https://github.com/user-attachments/assets/2e01b3cb-881a-47f2-95cc-d8e02e19c198)
>Ahora voy a acceder a la dirección https://172.17.0.2:443.

![Pasted image 20240722221915](https://github.com/user-attachments/assets/6a10c8c7-0634-4ff4-8cde-6e8bc5964109)
>Voy a aplicar fuzzing web con la herramienta dirb.

![Pasted image 20240722222500](https://github.com/user-attachments/assets/9e81131f-fabc-481f-84e7-249a69c31d8d)
>Encuentro el directorio uploads, que es donde se van a subir los archivos que suba desde el index.html.

![Pasted image 20240722222542](https://github.com/user-attachments/assets/3392722c-a2e9-41ba-9d67-3b4527d35cb7)
>Voy a intentar subir un archivo llamado reverse1.php para ver si me puede generar una reverse shell y poder así ganar acceso al sistema.
>Hago uso de la herramienta online [revshells](https://www.revshells.com/) para crear un script que me genere la reverse shell en php.

![Pasted image 20240722224446](https://github.com/user-attachments/assets/ed3f8959-d26b-459c-933b-9774be9fbce3)
>Creo el archivo, le subo, creo el servidor con Netcat para recibir la reverse shell y abro el archivo reverse1.php para obtener la reverse shell y ganar así acceso a la máquina.

![Pasted image 20240722224427](https://github.com/user-attachments/assets/bad37168-e965-4a56-8898-b37d1b63cd57)
>Voy a hacer un tratamiento de la tty.
```bash
script /dev/null -c bash
CTRL + z
stty raw -echo;fg
reset xterm
export TERM=xterm
exprt SHELL=bash
```
>Ahora voy a intentar iniciar sesión como el usuario mateo que me han dado antes y como contraseña voy a probar easycrxazy y también easycrazy ya que creo que la que he obtenido por algún casual está mal y pienso que será la segunda opción.

![Pasted image 20240722225345](https://github.com/user-attachments/assets/70ad936e-3597-40c8-920d-b9cfb43f9805)
>Consigo logearme como mateo con la contraseña easycrazy.
>Compruebo algunos directorios por si hubiese algo de contenido.

![Pasted image 20240722225524](https://github.com/user-attachments/assets/c5bf0755-e917-4f81-9774-bf136066c316)
>Como no encuentro nada listo los binarios para ver si hay alguno que pueda ejecutar como sudo y poder escalar privilegios.
>Encuentro que puedo ejecutar /usr/bin/php, por lo que con ayuda de la herramienta online [GTFOBins](https://gtfobins.github.io/gtfobins/php/#sudo), voy a intentar escalar privilegios y convertirme en root.

![Pasted image 20240722230052](https://github.com/user-attachments/assets/0076654e-e6b7-4ba8-803d-b4e9cdbfbe47)
