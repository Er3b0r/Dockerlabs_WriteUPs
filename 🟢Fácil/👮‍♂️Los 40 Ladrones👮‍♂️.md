
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240804173718.png]]
>Ahora procedo a realizar fuzzing web en busca de algún posible directorio oculto con la herramienta gobuster.
![[Pasted image 20240804174049.png]]
>Accedo al recurso qdefense.txt.
![[Pasted image 20240804174122.png]]
>Pienso que toctoc puede ser un posible usuario y 7000, 8000 y 9000 pueden ser posibles puertos.
![[Pasted image 20240804175909.png]]
>Como no obtengo nada, voy a probar a realizar un **port knocking** para ver si puedo abrir los puertos.
>[¿Qué es el PORT KNOCKING?](https://www.evaristogz.com/configurar-port-knocking-knock-ssh/)
>Port Knocking (traducido al español como «golpeo de puertos») es una de las **técnicas que se puede utilizar para securizar un servidor Linux**. Su funcionamiento es muy sencillo y permitiría que solo personas autorizadas accedan a un determinado puerto.
>Junto al uso de un servicio de cortafuegos por software, su principal función es evitar que los puertos queden expuestos, tanto a personas como a bots o escáneres automatizados de puertos.
>El usuario llama a una serie de puertos en un orden, por ejemplo al 2023, 2000, 9999 y el servicio de knockd habilitaría una regla en el firewall del sistema para permitir a la dirección IP solicitante el acceso al puerto o los puertos que hayamos configurado.
![[Pasted image 20240804180209.png]]
>Ahora se ha abierto el puerto 22 ssh.
>Voy a intentar iniciar sesión con el usuario toctoc y con hydra voy a utilizar un diccionario de contraseñas para mediante fuerza bruta intentar iniciar sesión.
![[Pasted image 20240804182346.png]]
>Inicio sesión al servicio ssh.
![[Pasted image 20240804182447.png]]
>Ahora voy a intentar escalar privilegios.
![[Pasted image 20240804183350.png]]
![[Pasted image 20240804183458.png]]
