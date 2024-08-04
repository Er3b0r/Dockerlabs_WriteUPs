Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.

![Pasted image 20240625224024](https://github.com/user-attachments/assets/c03390a3-e02a-44c0-8e8e-82a2616460e3)

El escaneo reporta que hay un servicio ftp al que nos podemos conectar como anonymous, un servicio ssh y un servicio apache.

Primeramente, me voy a conectar al servicio ftp como usuario anonymous y sin introducir contraseña.

Veo que hay dos archivos .txt disponibles por lo que procedo a descargarlos en mi máquina.

![Pasted image 20240625224007](https://github.com/user-attachments/assets/78f3a607-8f4d-4430-adb8-ab2ca8775b2e)

Una vez los he descargado, muestro el contenido de los archivos para ver si hay algo.

El archivo pendientes.txt habla en uno de sus puntos que hay ciertos permisos que no deberían de estar habilitados.

![Pasted image 20240625224056](https://github.com/user-attachments/assets/bb3dccf9-fc79-4329-960f-474ad8bace3a)

Ahora procedo a hacer fuzzing web a la dirección ip con la herramienta dirb.

Solamente me ha reportado una página index.html, un directorio /backup y otro directorio /important.

![Pasted image 20240625233143](https://github.com/user-attachments/assets/a41f5099-51d1-4651-9956-41739084d575)

Entro en el directorio backup y dentro encuentro un archivo backup.txt en el que se comenta que el usuario russoski es el mismo para todos los servicios.

![Pasted image 20240626135859](https://github.com/user-attachments/assets/e3d9baaa-3aca-4f1e-8dc2-6406dc4d4ce1)

Con la herramienta de hydra, voy a realizar un ataque de fuerza bruta al servicio ftp proporcionando el usuario russoski y un diccionario de contraseñas.

![Pasted image 20240625233529](https://github.com/user-attachments/assets/210ce111-5155-4201-a364-140f30eaeac8)

Una vez consigo las credenciales, inicio sesión e intento ver qué es lo que se encuentra dentro de este usuario.

![Pasted image 20240625233917](https://github.com/user-attachments/assets/9451dbbc-ae2f-4280-83d9-deb94868ffd1)

Encuentro una imagen .jpg, un README.md y un script en python.

En la imagen, no hay nada relevante, en el README.md tampoco y el script te genera una password de unos 20 caracteres mezclando letras, numeros y símbolos.

![Pasted image 20240625234001](https://github.com/user-attachments/assets/f800f5e9-d64d-44bf-a9f0-6cc553487722)

Ahora voy a probar las mismas credenciales que he utilizado para conectarme al ftp como sussoski pero esta vez al servicio ssh.

Una vez dentro, veo que tiene lo mismo que en el servicio ftp por lo que me dispongo a ver qué binarios puedo ejecutar como sudo pero si necesidad de introducir contraseña.

![Pasted image 20240625234453](https://github.com/user-attachments/assets/00a2078e-9012-497e-a147-122204a4a0e6)

Veo que puedo ejecutar /us/bin/vim por por lo que gracias a la herramienta [GTFObins](https://gtfobins.github.io/), introduzco un script que me va a permitir abrirme una consola sh como sudo gracias a ese binario.

Cuando ejecutamos el script ya soy root.

Una vez soy root, voy a ver qué es lo que tengo disponible y veo que hay un enlace a un video guardado en un .txt

![Pasted image 20240625234813](https://github.com/user-attachments/assets/3633682e-1f36-45c7-86fb-1b5bbca73480)
