Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240902190431](https://github.com/user-attachments/assets/480d6549-6103-4444-862f-f78e8c186e1c)

Accedo al recurso web http del puerto 80.

![Pasted image 20240902190611](https://github.com/user-attachments/assets/b93b4d08-8324-44cb-9b7c-dc052ad0b918)

Si selecciono la primera opción, voy a una web con diferentes imágenes.

Si observo el código fuente de esa web, puedo observar que en la parte inferior hay una cadena de texto hasheada.

![Pasted image 20240902190741](https://github.com/user-attachments/assets/2e08a619-4d46-4823-a850-62d7b87f94bd)

Voy a deshashear el mensaje.

![Pasted image 20240902190824](https://github.com/user-attachments/assets/37aa01c1-55b6-49f5-adb4-9083f8fe36fa)

Compruebo si esto podría ser un recurso web.

![Pasted image 20240902195949](https://github.com/user-attachments/assets/934b9dd1-914b-46ee-aee5-2b2b1f25a2e4)

Dentro del recurso encuentro un mensaje para un posible usuario lucas.

![Pasted image 20240902200023](https://github.com/user-attachments/assets/8ec03f9e-b8b7-4e21-9bad-8cfc7ce29416)

Intento obtener una contraseña para el posible usuario lucas con hydra.

![Pasted image 20240902200449](https://github.com/user-attachments/assets/4cef4902-5ee6-4c8d-9374-1d7c5efa2c0c)

Me conecto a la máquina víctima a través del servicio ssh.

![Pasted image 20240902200529](https://github.com/user-attachments/assets/393349d6-99f6-4798-b88d-d33c4b8697c3)

Intento escalar privilegios.

![Pasted image 20240902200904](https://github.com/user-attachments/assets/a948549b-5459-4b2b-a697-91a6e1e5cc76)

Ahora que soy el usuario andy, voy a intentar seguir escalando privilegios.

![Pasted image 20240902201435](https://github.com/user-attachments/assets/40eba5b7-79b1-4a55-b54e-e8ec79bd855b)

Ejecuto el primero ya que me llama mucho la atención su nombre.

![Pasted image 20240902201502](https://github.com/user-attachments/assets/811d068c-813f-4ae4-bd99-5c003fd75003)
