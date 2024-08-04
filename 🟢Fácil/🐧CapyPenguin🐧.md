Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240627195305](https://github.com/user-attachments/assets/8d3190dc-66b6-4a90-890e-f5c6bdf94538)

Realizo un escaneo de directorios utilizando la herramienta dirb indicando la url que deseo escanear y el puerto.

![Pasted image 20240627195616](https://github.com/user-attachments/assets/e3cd7c8c-0ce7-40fc-919a-21098bbc6803)

Accedo al servicio http, a simple vista no se ve nada útil.

![Pasted image 20240627195630](https://github.com/user-attachments/assets/d99156f8-a5a7-4036-adc3-7ae6be5a3111)

Decido mirar el código fuente por si hubiera algún mensaje oculto.

Encuentro un mensaje que dice que la contraseña se encuentra al final de un diccionario de contraseñas muy utilizado llamado rockyou y un posible usuario que sería capybarauser.

![Pasted image 20240627195656](https://github.com/user-attachments/assets/9927f184-ba14-431c-9288-e963a3171840)

Con el comando tac seguido del diccionario, mando el contenido pero del final al principio al archivo rockyou_reverse.txt.

![Pasted image 20240627200209](https://github.com/user-attachments/assets/6ab5e429-b158-429d-b5c3-a1820866fbb4)

Después de listar el contenido del archivo creado, tengo que realizar el siguiente comando ya que es necesario realizar ciertos ajustes, ya que por algún motivo no se ha copiado el contenido como debería.

![Pasted image 20240627201923](https://github.com/user-attachments/assets/d0378e99-3557-42fc-87f0-3ec0b524d428)

Una ver ajustado, procedo a realizar un ataque de fuerza bruta a la base de datos mysql de la dirección IP de la máquina, gracias a la herramienta hydra.

![Pasted image 20240627202002](https://github.com/user-attachments/assets/ad45300c-c9d1-427f-843d-4d4fc4a3da4f)

Encuentro una posible password para el posible usuario capybarauser.

Intento iniciar sesión en el servicio mysql.

Consigo entrar y procedo a listar las bases de datos disponibles.

![Pasted image 20240627203248](https://github.com/user-attachments/assets/eac28a35-b497-4da3-8541-a6b8a5d1d3e6)

Encuentro una base de datos interesante llamada pinguinaso_db.

Muestro sus tablas y veo que solamente tiene una que se llama users.

Listo el contenido de esa tabla y puedo ver que tiene los id, los nombres y las passwords de diferentes usuario.

![Pasted image 20240627203452](https://github.com/user-attachments/assets/d70330a8-cb98-43ab-8c50-bd9537f32bbb)

Realizo una consulta para ver los usuarios y las contraseñas de la tabla users.

![Pasted image 20240627203526](https://github.com/user-attachments/assets/5ac887b6-1303-436f-aa5a-3350edc4c40a)

Obtengo el usuario mario y la password pinguinomolon123.

Intento acceder al servicio ssh con esas credenciales.

![Pasted image 20240627203654](https://github.com/user-attachments/assets/0754f5da-b389-441c-a21f-9b48295fa067)

Una vez estoy dentro como usuario mario, intento ver qué binarios puedo ejecutar como sudo sin necesidad de utilizar contraseña.

![Pasted image 20240627204013](https://github.com/user-attachments/assets/6ce74069-2241-4e24-bd3e-8e984b61d190)

Puedo utilizar el binario /usr/bin/nano.

![Pasted image 20240627204719](https://github.com/user-attachments/assets/86068705-4e97-476b-b335-753c570e0ab1)

Cuando se nos abra el archivo con nano, hacemos CTRL + r y luego CTRL + x.

Luego ya escribo el siguiente comando.

He conseguido este comando gracias a la herramienta online [GTFObins](https://gtfobins.github.io/).

![Pasted image 20240627204611](https://github.com/user-attachments/assets/122bc174-bb41-4b2f-a3e2-d9ea9a713037)

Una vez ejecutado el comando, obtengo una shell como root

![Pasted image 20240627204627](https://github.com/user-attachments/assets/3e3af13b-5827-4f76-933d-6ddb6b918bef)

Hago un tratamiento de la consola para poder manejarme mejor con ella y ver si hay algún tipo de flag o mensaje.

Como no he encontrado nada más, finalizo la máquina.

![Pasted image 20240627204657](https://github.com/user-attachments/assets/995a22e9-cf71-482c-9fdc-1befd0f254da)
