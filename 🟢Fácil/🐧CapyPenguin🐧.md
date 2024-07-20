
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240627195305.png]]
>Realizo un escaneo de directorios utilizando la herramienta dirb indicando la url que deseo escanear y el puerto.
![[Pasted image 20240627195616.png]]
>Accedo al servicio http, a simple vista no se ve nada útil.
![[Pasted image 20240627195630.png]]
>Decido mirar el código fuente por si hubiera algún mensaje oculto.
>Encuentro un mensaje que dice que la contraseña se encuentra al final de un diccionario de contraseñas muy utilizado llamado rockyou y un posible usuario que sería capybarauser.
![[Pasted image 20240627195656.png]]
>Con el comando tac seguido del diccionario, mando el contenido pero del final al principio al archivo rockyou_reverse.txt.
![[Pasted image 20240627200209.png]]
>Después de listar el contenido del archivo creado, tengo que realizar el siguiente comando ya que es necesario realizar ciertos ajustes, ya que por algún motivo no se ha copiado el contenido como debería.
![[Pasted image 20240627201923.png]]
>Una ver ajustado, procedo a realizar un ataque de fuerza bruta a la base de datos mysql de la dirección IP de la máquina, gracias a la herramienta hydra.
![[Pasted image 20240627202002.png]]
>Encuentro una posible password para el posible usuario capybarauser.
>Intento iniciar sesión en el servicio mysql.
>Consigo entrar y procedo a listar las bases de datos disponibles.
![[Pasted image 20240627203248.png]]
>Encuentro una base de datos interesante llamada pinguinaso_db.
>Muestro sus tablas y veo que solamente tiene una que se llama users.
>Listo el contenido de esa tabla y puedo ver que tiene los id, los nombres y las passwords de diferentes usuario.
![[Pasted image 20240627203452.png]]
>Realizo una consulta para ver los usuarios y las contraseñas de la tabla users.
![[Pasted image 20240627203526.png]]
>Obtengo el usuario mario y la password pinguinomolon123.
>Intento acceder al servicio ssh con esas credenciales.
![[Pasted image 20240627203654.png]]
>Una vez estoy dentro como usuario mario, intento ver qué binarios puedo ejecutar como sudo sin necesidad de utilizar contraseña.
![[Pasted image 20240627204013.png]]
>Puedo utilizar el binario /usr/bin/nano.
![[Pasted image 20240627204719.png]]
>Cuando se nos abra el archivo con nano, hacemos CTRL + r y luego CTRL + x.
>Luego ya escribo el siguiente comando.
>He conseguido este comando gracias a la herramienta online GTFObins.
![[Pasted image 20240627204611.png]]  
>Una vez ejecutado el comando, obtengo una shell como root
![[Pasted image 20240627204627.png]]
>Hago un tratamiento de la consola para poder manejarme mejor con ella y ver si hay algún tipo de flag o mensaje.
>Como no he encontrado nada más, finalizo la máquina.
![[Pasted image 20240627204657.png]]