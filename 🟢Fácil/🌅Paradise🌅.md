Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240902190431.png]]
Accedo al recurso web http del puerto 80.
![[Pasted image 20240902190611.png]]
Si selecciono la primera opción, voy a una web con diferentes imágenes.
Si observo el código fuente de esa web, puedo observar que en la parte inferior hay una cadena de texto hasheada.
![[Pasted image 20240902190741.png]]
Voy a deshashear el mensaje.
![[Pasted image 20240902190824.png]]
Compruebo si esto podría ser un recurso web.
![[Pasted image 20240902195949.png]]
Dentro del recurso encuentro un mensaje para un posible usuario lucas.
![[Pasted image 20240902200023.png]]
Intento obtener una contraseña para el posible usuario lucas con hydra.
![[Pasted image 20240902200449.png]]
Me conecto a la máquina víctima a través del servicio ssh.
![[Pasted image 20240902200529.png]]
Intento escalar privilegios.
![[Pasted image 20240902200904.png]]
Ahora que soy el usuario andy, voy a intentar seguir escalando privilegios.
![[Pasted image 20240902201435.png]]
Ejecuto el primero ya que me llama mucho la atención su nombre.
![[Pasted image 20240902201502.png]]

