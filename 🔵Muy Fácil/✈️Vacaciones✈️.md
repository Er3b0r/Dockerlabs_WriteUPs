Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.

![Pasted image 20240625214349](https://github.com/user-attachments/assets/7188acc5-1757-484f-b01b-50aff032baee)

Accedo al servicio web de apache de la máquina.

![Pasted image 20240625214912](https://github.com/user-attachments/assets/9a146695-a049-4e71-9a95-af4ff14e69db)

A simple vista no vemos nada, pero si hacemos un **CTRL + u**, vemos lo siguiente.

![Pasted image 20240625214953](https://github.com/user-attachments/assets/0ae4c721-04e7-4646-b237-e0cb6e5868ab)

Ahora se nos ocurre que pueden ser dos usuarios de la máquina por lo que vamos a realizar una ataque por fuerza bruta al SSH.

![Pasted image 20240625215057](https://github.com/user-attachments/assets/b024a71f-3038-49d4-a694-b295c666f7ec)

Como anteriormente me he conectado a una máquina por SSH con esa misma IP, tengo que borrar del contenido **/home/kali/.ssh/know_hosts** la clave anterior.

![Pasted image 20240625214849](https://github.com/user-attachments/assets/de8fda77-3a91-47a7-97b8-be21b227cb4a)

Me conecto con las credenciales que he obtenido y ya estoy dentro.

![Pasted image 20240625215223](https://github.com/user-attachments/assets/78f2a72a-6d39-4c4f-b8f5-b4cc63ae1714)

Buscamos en los directorios a los que tenemos acceso y encontramos un correo con una contraseña.

![captura_1720433021](https://github.com/user-attachments/assets/086d3a4d-272d-4ddd-af81-8e538e241309)

Probamos la contraseña que hemos obtenido con el usuario juan y conseguimos acceso.

![captura_1720433204](https://github.com/user-attachments/assets/7ffd4333-1932-42c3-a3ac-ad8c056f8832)

Voy a intentar escalar privilegios buscando a ver si puedo ejecutar algún binario como sudo sin necesidad de utilizar contraseña.

Veo que puedo ejecutar el binario ruby.

![captura_1720433287](https://github.com/user-attachments/assets/4fde75d1-e0fa-4ab1-acf0-716a309815b3)

Haciendo uso de una herramienta online GTFObins, busco algún script que me pueda ayudar a escalar privilegios.

Ejecuto el script y ya soy root.

![captura_1720433428](https://github.com/user-attachments/assets/6caa7541-7f2e-4025-8ce9-1d6cf72d805a)
