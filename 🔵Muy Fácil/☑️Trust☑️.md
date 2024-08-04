Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.

![Pasted image 20240616182731](https://github.com/user-attachments/assets/d79c2629-802a-41f0-a6d1-21c1847e25fb)

Ahora mediante la herramienta gobuster, voy a hacer fuzzing para ver a qué otras direcciones podemos acceder dentro de esa web.

![Pasted image 20240616183532](https://github.com/user-attachments/assets/17d621ac-d20d-48aa-9add-da18790b6eb7)

Entro en la que me llama un poco la atención sobre todo por su nombre secret.php.

![Pasted image 20240616183620](https://github.com/user-attachments/assets/f224368f-525b-44c5-98d7-b8aae149dd50)

Encuentro un posible usuario llamado mario.

Decido hacer fruerza bruta al servicio ssh con un diccionario de contraseñas y empleando el usuario mario.

![Pasted image 20240616184244](https://github.com/user-attachments/assets/62798cda-d542-4eb2-b551-95af0b47618c)

Estoy dentro como usuario mario y ahora me dispongo a escalar privilegios.

Voy a utulizar la herramienta online [GTFObins](https://gtfobins.github.io/gtfobins/vim/#sudo) y utilizaré el siguiente comando ya que tengo permisos como root sin necesidad de introducir password sobre ese binario.

![Pasted image 20240616184921](https://github.com/user-attachments/assets/a8aaf867-e116-4fdd-8730-e70e4ade50e4)
