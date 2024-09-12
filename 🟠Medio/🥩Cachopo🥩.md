
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240912205450.png]]
Accedo al recurso web del puerto 80 y me encuentro con una web de un restaurante.
Abajo de la web hay como una especie de formulario para hacer una reserva.
![[Pasted image 20240912205625.png]]
Realizo un escaneo de directorios con gobuster pero recibo muchos mensajes de error por lo que decido hacer otra cosa.
Voy a utilizar BurpSuite para mandar una petición del formulario, interceptarla y ver qué pasa.
Configuro el proxy, relleno los datos y mando la petición para recibirla con BurpSuite.
![[Pasted image 20240912210635.png]]
Con el Repeater, si envío la petición recibo el siguiente error.
![[Pasted image 20240912211118.png]]
Buscando el error en el navegador, encuentro que puede ser un error dado porque se puede estar intentando decodear el `userInput` por lo que voy a probar a codificar en base-64 una cadena de caracteres y ver qué me devuelve BurpSuite.
![[Pasted image 20240912211858.png]]
![[Pasted image 20240912211922.png]]
Recibo otro error, por lo que deduzco que estaba en lo correcto y  está intentando decodear el `userInput`.
Voy a intentar listar el `/etc/passwd`.
![[Pasted image 20240912212124.png]]
![[Pasted image 20240912212138.png]]
Recibo el archivo `/etc/passwd`.
Esto demuestra que puedo inyectar comandos.
![[Pasted image 20240912212213.png]]
Voy a intentar obtener la contraseña del usuario cachopin con hydra para posteriormente iniciar sesión por ssh.
![[Pasted image 20240912212338.png]]
Una vez inicio como cachopin, encuentro un archivo con varios hashes.
![[Pasted image 20240912214016.png]]
Busco en el navegador alguna herramienta que me ayude pero no encuentro nada por lo que decido ir al GitHub del creador de la máquina ([PatxaSec](https://github.com/PatxaSec/SHA_Decrypt)) para ver si este tiene alguna herramienta que me ayude.
![[Pasted image 20240912214317.png]]
Clono la herramienta en mi máquina atacante.
Voy probando cada hash para ver si encuentro alguna password.

Consigo encontrar una password `cecina`.
![[Pasted image 20240912214936.png]]
Prueba esa contraseña para ser el usuario root.
![[Pasted image 20240912215027.png]]
