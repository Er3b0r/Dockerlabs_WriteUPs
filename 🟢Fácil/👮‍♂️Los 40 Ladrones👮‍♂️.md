>Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240804173718](https://github.com/user-attachments/assets/40eb51fc-fa86-416c-94f5-58219d4e5247)
>Ahora procedo a realizar fuzzing web en busca de algún posible directorio oculto con la herramienta gobuster.

![Pasted image 20240804174049](https://github.com/user-attachments/assets/7ebda538-9ac6-4593-b030-c853fb38911d)
>Accedo al recurso qdefense.txt.

![Pasted image 20240804174122](https://github.com/user-attachments/assets/80e94b86-fb68-49e4-883c-647f97ed94c7)
>Pienso que toctoc puede ser un posible usuario y 7000, 8000 y 9000 pueden ser posibles puertos.

![Pasted image 20240804175909](https://github.com/user-attachments/assets/471d6aa4-bc4c-4722-ab1d-0e916133fce1)
>Como no obtengo nada, voy a probar a realizar un **port knocking** para ver si puedo abrir los puertos.

>[¿Qué es el PORT KNOCKING?](https://www.evaristogz.com/configurar-port-knocking-knock-ssh/)
>Port Knocking (traducido al español como «golpeo de puertos») es una de las **técnicas que se puede utilizar para securizar un servidor Linux**. Su funcionamiento es muy sencillo y permitiría que solo personas autorizadas accedan a un determinado puerto.
>Junto al uso de un servicio de cortafuegos por software, su principal función es evitar que los puertos queden expuestos, tanto a personas como a bots o escáneres automatizados de puertos.
>El usuario llama a una serie de puertos en un orden, por ejemplo al 2023, 2000, 9999 y el servicio de knockd habilitaría una regla en el firewall del sistema para permitir a la dirección IP solicitante el acceso al puerto o los puertos que hayamos configurado.

![Pasted image 20240804180209](https://github.com/user-attachments/assets/719084ad-d3e5-4ae0-b8ab-57a8aa7d88e5)
>Ahora se ha abierto el puerto 22 ssh.
>Voy a intentar iniciar sesión con el usuario toctoc y con hydra voy a utilizar un diccionario de contraseñas para mediante fuerza bruta intentar iniciar sesión.

![Pasted image 20240804182346](https://github.com/user-attachments/assets/ae681e8f-a4dd-4a64-9f71-eab9a5708853)
>Inicio sesión al servicio ssh.

![Pasted image 20240804182447](https://github.com/user-attachments/assets/a97e1d62-87aa-4856-9c09-6dbc0be428ce)
>Ahora voy a intentar escalar privilegios.

![Pasted image 20240804183350](https://github.com/user-attachments/assets/02dec558-09c6-4d35-9df9-614ef64e82e5)
![Pasted image 20240804183458](https://github.com/user-attachments/assets/99961515-10ef-473d-a3c1-5e4b730a1905)
