
Nmap
![[Pasted image 20240805021806.png]]
Inicio como anonymous al servicio ftp.
Descargo el archivo.
![[Pasted image 20240805022241.png]]
Intento descomprimir el archivo pero tiene una password.
![[Pasted image 20240805022331.png]]
Voy a usar john the ripper para intentar crackear la password.
![[Pasted image 20240805022732.png]]
Ahora puedo descomprimir el archivo zip con la contraseña password1.
![[Pasted image 20240805023114.png]]
Obtengo el archivo password.txt con un usuario y una contraseña con los que probablemente pueda iniciar sesión por ssh.
![[Pasted image 20240805023209.png]]
![[Pasted image 20240805023347.png]]
Ahora voy a intentar escalar privilegios.
![[Pasted image 20240805024153.png]]
Modifico el contenido de script.js con código javascript para obtener una reverse shell gracias a la herramienta online [GTFOBins](https://gtfobins.github.io/gtfobins/node/#reverse-shell).
![[Pasted image 20240805024339.png]]
Me pongo en escucha por el puerto indicado y ejecuto el script de la siguiente manera.
```bash
sudo /usr/bin/node /home/mario/script.js
```
![[Pasted image 20240805024322.png]]