
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240810005555.png]]
Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.
![[Pasted image 20240810010103.png]]
Reviso el código fuente del index por si hubiese algo oculto.
![[Pasted image 20240810010244.png]]
Accedo al recurso autentication.js.
![[Pasted image 20240810010321.png]]
Si ahora voy al recurso de /backend/server.js veo que la petición la tramita por post.
![[Pasted image 20240810010722.png]]
Puedo comprobar que la contraseña es la correcta ejecutado el siguiente comando con curl.
![[Pasted image 20240810011245.png]]
Ahora voy a realizar un ataque de fuerza bruta al servicio ssh indicando el puerto 5000 ya que sino le indico por defecto utiliza el 22.
![[Pasted image 20240810011534.png]]
Ahora inicio sesión por ssh indicando el puerto 5000 ya que sino le indico por defecto utiliza el 22.
![[Pasted image 20240810011648.png]]
Voy a intentar escalar privilegios.
![[Pasted image 20240810012008.png]]
Dentro del editor de texto nano ejecuto lo siguiente.
```
script /dev/null -c bash
Control + R
Control + X
reset; sh 1>&0 2>&0
```
Me deja ejecutar los comandos como root dentro del editor de texto como se ve en la siguiente imagen.
![[Pasted image 20240810011947.png]]
