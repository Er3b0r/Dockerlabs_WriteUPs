
---
>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.
![[Pasted image 20240625224024.png]]
>El escaneo reporta que hay un servicio ftp al que nos podemos conectar como anonymous, un servicio ssh y un servicio apache.
>Primeramente, me voy a conectar al servicio ftp como usuario anonymous y sin introducir contraseña.
>Veo que hay dos archivos .txt disponibles por lo que procedo a descargarlos en mi máquina.
![[Pasted image 20240625224007.png]]
>Una vez los he descargado, muestro el contenido de los archivos para ver si hay algo.
>El archivo pendientes.txt habla en uno de sus puntos que hay ciertos permisos que no deberían de estar habilitados.
![[Pasted image 20240625224056.png]]
>Ahora procedo a hacer fuzzing web a la dirección ip con la herramienta dirb.
>Solamente me ha reportado una página index.html, un directorio /backup y otro directorio /important.
![[Pasted image 20240625233143.png]]
>Entro en el directorio backup y dentro encuentro un archivo backup.txt en el que se comenta que el usuario russoski es el mismo para todos los servicios.
![[Pasted image 20240626135859.png]]
>Con la herramienta de hydra, voy a realizar un ataque de fuerza bruta al servicio ftp proporcionando el usuario russoski y un diccionario de contraseñas.
![[Pasted image 20240625233529.png]]
>Una vez consigo las credenciales, inicio sesión e intento ver qué es lo que se encuentra dentro de este usuario.
![[Pasted image 20240625233917.png]]
>Encuentro una imagen .jpg, un README.md y un script en python.
>En la imagen, no hay nada relevante, en el README.md tampoco y el script te genera una password de unos 20 caracteres mezclando letras, numeros y símbolos.
![[Pasted image 20240625234001.png]]
>Ahora voy a probar las mismas credenciales que he utilizado para conectarme al ftp como sussoski pero esta vez al servicio ssh.
>Una vez dentro, veo que tiene lo mismo que en el servicio ftp por lo que me dispongo a ver qué binarios puedo ejecutar como sudo pero si necesidad de introducir contraseña.
![[Pasted image 20240625234453.png]]
>Veo que puedo ejecutar /us/bin/vim por por lo que gracias a la herramienta GTFObins, introduzco un script que me va a permitir abrirme una consola sh como sudo gracias a ese binario.
>Cuando ejecutamos el script ya soy root.
>Una vez soy root, voy a ver qué es lo que tengo disponible y veo que hay un enlace a un video guardado en un .txt
![[Pasted image 20240625234813.png]]
