
---
>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.
![[Pasted image 20240625222311.png]]
>Obtengo la información de que hay un servicio ssh y otro http.
>Voy a acceder primero al servicio http para ver que tiene.
>Encuentro una imagen y procedo a descargarla.
![[Pasted image 20240625222323.png]]
>Una vez descargada la imagen, voy a utilizar la herramienta exiftool para poder ver los metadatos de la imagen, por si hubiese algo importante.
>Cuando obtengo la información, puedo ver que hay un posible usuario y una posible contraseña.
![[Pasted image 20240625222341.png]]
>Voy a realizar un ataque de fuerza bruta al servicio ssh con el posible usuario que he obtenido.
![[Pasted image 20240625222505.png]]
>Con las credenciales que he obtenido utilizando la herramienta de hydra, consigo iniciar sesión en el servicio ssh.
![[Pasted image 20240625222530.png]]
>Listo los binarios que puedo ejecutar como sudo sin necesidad de utilizar contraseña y veo que puedo utilizar /bin/bash.
>Simplemente ejecutando sudo /bin/bash ya obtenemos una consola como usuario root por lo que abríamos escalado privilegios de una forma muy fácil.
![[Pasted image 20240625222653.png]]
![[Pasted image 20240625222732.png]]
