
---
>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.
Pasted image 20240616182731.png(https://github.com/user-attachments/assets/28c5ffc2-22f0-40f5-9de0-233460aa8e2f)

>Ahora mediante la herramienta gobuster, voy a hacer fuzzing para ver a qué otras direcciones podemos acceder dentro de esa web.
![[Pasted image 20240616183532.png]]
>Entro en la que me llama un poco la atención sobre todo por su nombre secret.php.
![[Pasted image 20240616183620.png]]
>Encuentro un posible usuario llamado mario.
>Decido hacer fruerza bruta al servicio ssh con un diccionario de contraseñas y empleando el usuario mario.
![[Pasted image 20240616184244.png]]
>Estoy dentro como usuario mario y ahora me dispongo a escalar privilegios.
>Voy a utulizar la herramienta online [GTFObins](https://gtfobins.github.io/gtfobins/vim/#sudo) y utilizaré el siguiente comando ya que tengo permisos como root sin necesidad de introducir password sobre ese binario.
![[Pasted image 20240616184921.png]]

