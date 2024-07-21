>Lo primero es hacer un escaneo de puertos y servicios con nmap.

![captura_1720213330](https://github.com/user-attachments/assets/cd6796ee-236d-4994-92b6-440411378bba)
>Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.

![captura_1720213550](https://github.com/user-attachments/assets/c7ee8ad2-7988-48c8-abfb-ab65d513f855)
>Intento acceder al directorio javascript pero el servidor me reporta que no tengo los permisos adecuados para acceder al recurso.

![captura_1720213561](https://github.com/user-attachments/assets/4a855222-260b-4e92-98de-79d2f30a916e)
>Accedo al index.php y encuentro un string de caracteres que podrían ser una password.

![captura_1720213584](https://github.com/user-attachments/assets/f9f27bb6-8477-4799-8cb9-34733ee5fb27)
>Voy a realizar un ataque de fuerza bruta al servicio ssh proporcionando la supuesta password y utilizando un diccionario usuarios/passwords para intentar obtener el usuario válido.

![captura_1720213939](https://github.com/user-attachments/assets/17e971b7-4748-4414-a479-8c746540e570)
>Una vez obtengo las credenciales, compruebo que sean válidas intentando acceder al servicio ssh.

![captura_1720214088](https://github.com/user-attachments/assets/fe29a005-d43a-49f6-bd1f-2ccf55c6b36a)
>Consigo acceder como carlos.
>Compruebo a ver qué binarios puedo ejecutar como sudo y veo que puedo ejecutar el binario /usr/bin/python3 sobre el script /opt/script.py.
>Voy a realizar un tratamiento de la consola del terminal para operar con ella de manera más sencilla.
```bash
export TERM=xterm
export SHELL=bash
```
>Muestro el contenido del script de python script.py.
>Veo que importa una librería de python llamada shutil.
>Se me ocurre crear un script en python llamado shutil.py, y dentro de este importar la librería os para poder ejecutar un script que de permisos de SUID a /bin/bash.

![captura_1720216963](https://github.com/user-attachments/assets/ef498fae-4ab3-4702-a2c8-d8f73c508281)
>Como vemos el script de python importa la librería shutil, aprovecho eso para crear un fichero de python que ejecute código a nivel de sistema, para poder dar privilegios a la bash y poder ejecutarla como root.
>Ejecuto el script que me permitirá ganar privilegios.

![captura_1720217089](https://github.com/user-attachments/assets/74c16134-3ec8-47e5-a34a-8c0777322c7d)
>He conseguido dar privilegios SUID a la bash.

![captura_1720217332](https://github.com/user-attachments/assets/c94a9b26-a5cb-4a7c-af29-c1605d14c163)
