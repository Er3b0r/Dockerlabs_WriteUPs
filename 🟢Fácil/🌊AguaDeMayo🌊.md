
---
>Escaneo de puertos y servicios.
![[Pasted image 20240721182946.png]]
>Fuzzing web con gobuster.
![[Pasted image 20240721183635.png]]
>Si accedo al código fuente del index, encuentro comentado el siguiente código.
![[Pasted image 20240721184416.png]]
>Si lo copio y pego en Google, veo que se trata de un código brainfuck, por lo que voy a hacer uso de un decoder online.
![[Pasted image 20240721184837.png]]
>Ahora accedo al recurso images para ver que hay y encuentro una imagen.
![[Pasted image 20240721183718.png]]
>Descargo la imagen y pruebo con varias herramientas de esteganografía pero no encuentro nada.
>Procedo entonces a acceder mediante ssh, utilizando como usuario agua y como contraseña la que obtuvimos al decodear el mensaje en brainfuck (bebeaguaqueessano).
![[Pasted image 20240721185808.png]]
>Voy a intentar escalar privilegios para ello voy a ver si hay algún binario que pueda ejecutar como sudo.
![[Pasted image 20240721192711.png]]
>Ejecuto como sudo /usr/bin/bettercap
>Si pongo help veo que puedo ejecutar comandos si primero pongo el signo !.
![[Pasted image 20240721192822.png]]
>Veo que soy el usuario root.
![[Pasted image 20240721192848.png]]
>Voy a intentar darme privilegios de SUID a la bash para ejecutarla con el usuario agua y poder ser root.
![[Pasted image 20240721193126.png]]