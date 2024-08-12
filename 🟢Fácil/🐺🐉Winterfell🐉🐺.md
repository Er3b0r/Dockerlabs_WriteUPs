
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240812213740.png]]
Accedo al recurso http del puerto 80.
![[Pasted image 20240812214748.png]]
Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.
![[Pasted image 20240812214215.png]]
En la dirección obtenida encuentro lo siguiente.
![[Pasted image 20240812214238.png]]
Copiamos los nombres de los episodios en un archivo txt.
![[Pasted image 20240812214634.png]]
Tenemos 3 supuestos usuarios, Jon, Arya y Daenerys y puede que la contraseña de alguno de ellos sea uno de los nombres de los episodios.
Ahora voy a intentar sacar la contraseña de alguno de los usuarios anteriores para el servicio smb.
Utilizo crackmapexec para obtener la contraseña.
![[Pasted image 20240812215240.png]]
Con smbmap voy a intentar enumerar los recursos compartidos en smb por el usuario jon.
![[Pasted image 20240812215724.png]]
Ahora con smbclient voy a tratar de descargar el contenido que me pueda ser útil.
Muestro el contenido del archivo que descargo.
![[Pasted image 20240812220721.png]]
Me dan una contraseña cifrada en base64.
![[Pasted image 20240812220808.png]]
Con la contraseña inicio sesión en ssh como jon.
![[Pasted image 20240812220902.png]]
En el directorio home veo el siguiente contenido.
![[Pasted image 20240812221025.png]]
Voy a intentar escalar privilegios con ayuda de los binarios.
![[Pasted image 20240812222043.png]]
Se me ocurre cambiar el contenido del archivo .mensaje.py, pero no tengo los permisos, por lo que con el comando mv, le cambio el nombre a mensaje.py, con echo modifico el contenido y creo un script que me proporciona una bash, vuelvo a nombrar el mensaje.py como .mensaje.py.
![[Pasted image 20240812222309.png]]
Al final me toca cambiar el contenido porque no se me añadieron bien las comillas, por lo que quedaría de la siguiente forma.
```bash
mv .mensaje.py mensaje.py
echo -e 'import os\nos.system(\"/bin/bash\")' > mensaje.py
mv mensaje.py .mensaje.py
```
Si ahora ejecuto el siguiente comando me convierto en el usuario aria.
![[Pasted image 20240812222712.png]]
Intento seguir escalando privilegios con ayuda de los binarios y encuentro en el directorio /home/daenerys un archivo con el siguiente contenido.
![[Pasted image 20240812223142.png]]
Con la contraseña drakaris me puedo logear como daenerys.
![[Pasted image 20240812223305.png]]
Intento seguir escalando privilegios con ayuda de los binarios.
![[Pasted image 20240812223441.png]]
Ahora modifico el contenido del script .shell.sh para proporcionarme una reverse shell a mi máquina atacante.
![[Pasted image 20240812224220.png]]
Antes de ejecutar el comando anterior sudo, debo de ponerme en escucha.
Una vez escuchando por el puerto indicado, ejecuto el script y recibo la conexión.
![[Pasted image 20240812224231.png]]