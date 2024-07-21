>Escaneo de puertos y servicios con nmap.

![Pasted image 20240721182946](https://github.com/user-attachments/assets/3d922df6-2e72-4ff1-b953-e20d83617a70)
>Fuzzing web con gobuster.

![Pasted image 20240721183635](https://github.com/user-attachments/assets/69c9e54b-12fa-4dbe-8b15-780568c63956)
>Si accedo al código fuente del index, encuentro comentado el siguiente código.

![Pasted image 20240721184416](https://github.com/user-attachments/assets/945cb277-354b-4165-a5c3-67af600fa0d4)
>Si lo copio y pego en Google, veo que se trata de un código brainfuck, por lo que voy a hacer uso de un decoder online.

![Pasted image 20240721184837](https://github.com/user-attachments/assets/024f3dfd-3276-42e7-9dc9-12385ba87bf7)
>Ahora accedo al recurso images para ver que hay y encuentro una imagen.

![Pasted image 20240721183718](https://github.com/user-attachments/assets/2f0ea04c-90c2-4aa2-8231-b41e554efda7)
>Descargo la imagen y pruebo con varias herramientas de esteganografía pero no encuentro nada.
>Procedo entonces a acceder mediante ssh, utilizando como usuario agua y como contraseña la que obtuvimos al decodear el mensaje en brainfuck (bebeaguaqueessano).

![Pasted image 20240721185808](https://github.com/user-attachments/assets/91e401de-e53d-4707-88dc-76162aa54b96)
>Voy a intentar escalar privilegios para ello voy a ver si hay algún binario que pueda ejecutar como sudo.

![Pasted image 20240721192711](https://github.com/user-attachments/assets/18ceb159-f501-4bdd-81fe-ff87cbc47154)
>Ejecuto como sudo /usr/bin/bettercap
>Si pongo help veo que puedo ejecutar comandos si primero pongo el signo !.

![Pasted image 20240721192822](https://github.com/user-attachments/assets/08c4b7be-41a1-4846-ba2f-04b3a42c1f8d)
>Veo que soy el usuario root.

![Pasted image 20240721192848](https://github.com/user-attachments/assets/8703e2b9-fab9-4513-9919-df1fdfc8742e)
>Voy a intentar darme privilegios de SUID a la bash para ejecutarla con el usuario agua y poder ser root.

![Pasted image 20240721193126](https://github.com/user-attachments/assets/956a67ae-b3e0-46f1-b579-9e92108fa173)
