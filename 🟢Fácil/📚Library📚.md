
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[captura_1720213330.png]]
>Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.
![[captura_1720213550.png]]
>Intento acceder al directorio javascript pero el servidor me reporta que no tengo los permisos adecuados para acceder al recurso.
![[captura_1720213561.png]]
>Accedo al index.php y encuentro un string de caracteres que podrían ser una password.
![[captura_1720213584.png]]
>Voy a realizar un ataque de fuerza bruta al servicio ssh proporcionando la supuesta password y utilizando un diccionario usuarios/passwords para intentar obtener el usuario válido.
![[captura_1720213939.png]]
>Una vez obtengo las credenciales, compruebo que sean válidas intentando acceder al servicio ssh.
![[captura_1720214088.png]]
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
![[captura_1720216963.png]]
Como vemos el script de python importa la librería shutil, aprovecho eso para crear un fichero de python que ejecute código a nivel de sistema, para poder dar privilegios a la bash y poder ejecutarla como root.
Ejecuto el script que me permitirá ganar privilegios.
![[captura_1720217089.png]]
He conseguido dar privilegios SUID a la bash.
![[captura_1720217332.png]]
