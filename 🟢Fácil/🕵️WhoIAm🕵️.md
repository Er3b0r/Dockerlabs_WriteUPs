
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240812001812.png]]
Accedo a la web.
![[Pasted image 20240812001852.png]]
Hago fuzzing web con gobuster.
![[Pasted image 20240812002256.png]]
Si accedo a la dirección /wp-admin/ encuentro un panel de login de WordPress.
![[Pasted image 20240812002307.png]]
Como no tengo como iniciar sesión, voy a seguir buscando.
En la dirección /backups/, encuentro un archivo zip que procedo a descargar para ver su contenido.
![[Pasted image 20240812002546.png]]
Descargo el archivo, lo descomprimo y veo su contenido.
![[Pasted image 20240812002654.png]]
Ahora ya tenemos el usuario y la contraseña para iniciar sesión en wordpress.
![[Pasted image 20240812002812.png]]
Voy a intentar buscar vulnerabilidades de los plugins que posea este wordpress, para ello primero debo saber qué plugins tiene.
![[Pasted image 20240812005442.png]]
Encuentro el siguiente plugin.
![[Pasted image 20240812005522.png]]
Lo siguiente es buscar algún exploit con searchsploit.
![[Pasted image 20240812005614.png]]
Descargo el exploit.
![[Pasted image 20240812005740.png]]
Ejecuto el siguiente comando para crear una shell en el navegador.
![[Pasted image 20240812010609.png]]
Si ahora accedo a la URL que indica veo lo siguiente.
![[Pasted image 20240812010638.png]]
Me envío una reverse shell.
![[Pasted image 20240812012330.png]]
Ahora tengo que intentar escalar privilegios, esto lo voy a intentar con los binarios del sistema.
![[Pasted image 20240812012730.png]]
Sigo intentando escalar privilegios.
![[Pasted image 20240812012925.png]]
Ahora voy a intentar ganar acceso a root con ayuda de los binarios.
Veo que puedo ejecutar un script.
```bash
#!/bin/bash
read -rp "Enter guess: " num

if [[ $num -eq 42 ]]
then
  echo "Correct"
else
  echo "Wrong"
fi
```
Ese script me devuelve correcto si el número que aporto es 42, por lo que se me ocurre ejecutar el siguiente script, que lo que hace es dar permisos SUID a la ruta /bin/bash, este valor se lo asigna a la variable prueba y le sumamos el numero 42 para que no de error.
```bash
prueba[$(chmod u+s /bin/bash >&2)]+42
```
De esta manera puedo ahora ejecutar el comando bash -p que me proporciona una bash como root.
![[Pasted image 20240812014749.png]]
