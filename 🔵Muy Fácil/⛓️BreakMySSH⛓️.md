>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.

![Pasted image 20240625174454](https://github.com/user-attachments/assets/ed997ca5-5f1c-4400-961e-9d2e4979bf13)
>Hay dos maneras de resolver esta máquina, voy a explicar ambas.

---
## Hydra Bruteforce
>Voy a utilizar un ataque de fuerza bruta con hydra al servicio ssh, ya que no tengo ninguna información, probaré con el usuario root a ver si hay suerte y un diccionario de contraseñas.

![Pasted image 20240625174523](https://github.com/user-attachments/assets/c8d4f875-2fc5-4acb-a0dd-5c1f3e2a492d)

>Obtengo las credenciales y accedo como root al ssh.

![Pasted image 20240625174607](https://github.com/user-attachments/assets/9c77890b-f9c9-4878-baa7-f57ebe535df9)

---
## MSFCONSOLE
>Suponiendo que ya he hecho el escaneo con nmap, abro metasploit.

![Pasted image 20240625213112](https://github.com/user-attachments/assets/26459af2-b63f-42c6-9bf0-7593588a740b)
>Busco a ver si hay algún script relacionado con OpenSSH.
>Selecciono el numero 3 ya que me interesa listar los posibles usuarios de ese servicio.

![Pasted image 20240625213145](https://github.com/user-attachments/assets/b62a790e-e084-4100-8014-4f602516e92c)
>Configuro el script con los siguientes parámetros, indicando el host de destino, el archivo de diccionario de usuarios que va a utilizar y el puerto si fuese necesario, en este caso no lo es.
>Lanzo el script y ya me reporta varios posibles usuarios.

![Pasted image 20240625213209](https://github.com/user-attachments/assets/90b977e6-124b-43a0-b0d3-206f4ed5e292)
>Paramos el script ya que he utilizado un diccionario muy extenso y tarda mucho.
>Ahora tenemos unos cuantos usuarios, probamos con root como en el ejemplo anterior utilizando hydra y el mismo diccionario de contraseñas.
>Conseguimos acceso por SSH al usuario root y vamos a listar el archivo **/etc/passwd** para ver si coinciden los usuarios que hemos sacado con el exploit.

![Pasted image 20240625213452](https://github.com/user-attachments/assets/81b703e1-a601-4a19-8dee-2597109020a3)
>Como podemos apreciar, si que hay usuarios que coinciden y probablemente hubiésemos conseguido obtener el resto pero paramos el exploit por su gran demora de tiempo.
