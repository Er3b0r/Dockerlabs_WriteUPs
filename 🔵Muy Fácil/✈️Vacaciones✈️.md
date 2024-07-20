
---
>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.
![[Pasted image 20240625214349.png]]
>Accedo al servicio web de apache de la máquina.
![[Pasted image 20240625214912.png]]
>A simple vista no vemos nada, pero si hacemos un **CTRL + u**, vemos lo siguiente.
![[Pasted image 20240625214953.png]]
>Ahora se nos ocurre que pueden ser dos usuarios de la máquina por lo que vamos a realizar una ataque por fuerza bruta al SSH.
![[Pasted image 20240625215057.png]]
>Como anteriormente me he conectado a una máquina por SSH con esa misma IP, tengo que borrar del contenido **/home/kali/.ssh/know_hosts** la clave anterior.
![[Pasted image 20240625214849.png]]
>Me conecto con las credenciales que he obtenido y ya estoy dentro.
![[Pasted image 20240625215223.png]]
>Buscamos en los directorios a los que tenemos acceso y encontramos un correo con una contraseña.
![[captura_1720433021.png]]
>Probamos la contraseña que hemos obtenido con el usuario juan y conseguimos acceso.
![[captura_1720433204.png]]
>Voy a intentar escalar privilegios buscando a ver si puedo ejecutar algún binario como sudo sin necesidad de utilizar contraseña.
>Veo que puedo ejecutar el binario ruby.
![[captura_1720433287.png]]
>Haciendo uso de una herramienta online GTFObins, busco algún script que me pueda ayudar a escalar privilegios.
>Ejecuto el script y ya soy root.
![[captura_1720433428.png]]