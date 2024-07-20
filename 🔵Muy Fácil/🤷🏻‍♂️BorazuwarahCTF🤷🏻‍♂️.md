>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.

![Pasted image 20240625222311](https://github.com/user-attachments/assets/bb71d73e-8f4b-47a2-9c4e-0419984d3254)
>Obtengo la información de que hay un servicio ssh y otro http.
>Voy a acceder primero al servicio http para ver que tiene.
>Encuentro una imagen y procedo a descargarla.

![Pasted image 20240625222323](https://github.com/user-attachments/assets/c29dc8c9-34e6-4ebe-8127-8a07d3f88a7a)
>Una vez descargada la imagen, voy a utilizar la herramienta exiftool para poder ver los metadatos de la imagen, por si hubiese algo importante.
>Cuando obtengo la información, puedo ver que hay un posible usuario y una posible contraseña.

![Pasted image 20240625222341](https://github.com/user-attachments/assets/7d0d3374-b409-4764-b7d2-944ef0382b37)
>Voy a realizar un ataque de fuerza bruta al servicio ssh con el posible usuario que he obtenido.

![Pasted image 20240625222505](https://github.com/user-attachments/assets/9ea177eb-cfc4-4f68-905c-ee257c431cc3)
>Con las credenciales que he obtenido utilizando la herramienta de hydra, consigo iniciar sesión en el servicio ssh.

![Pasted image 20240625222530](https://github.com/user-attachments/assets/64b9c2e6-3907-4f7a-9f8e-b86db825e058)
>Listo los binarios que puedo ejecutar como sudo sin necesidad de utilizar contraseña y veo que puedo utilizar /bin/bash.
>Simplemente ejecutando sudo /bin/bash ya obtenemos una consola como usuario root por lo que abríamos escalado privilegios de una forma muy fácil.

![Pasted image 20240625222653](https://github.com/user-attachments/assets/a378cf85-30fd-4d71-a132-08346d409fc1)
![Pasted image 20240625222732](https://github.com/user-attachments/assets/9efb75c7-736b-4655-aa24-8d20cc250c07)
