Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20241001213948](https://github.com/user-attachments/assets/d04705ca-ad80-4bcb-a3b8-1acae079e784)

Accedo al recurso web del puerto 80.

![Pasted image 20241001214017](https://github.com/user-attachments/assets/cef711e1-8db5-4650-a7c8-026fa5b4d682)

Voy a realizar un escaneo de directorios con `gobuster`.

![Pasted image 20241001214314](https://github.com/user-attachments/assets/bdec63db-f47c-4499-bfde-fdd8a9118093)

Encuentro que hay un directorio llamado `wordpress`.

![Pasted image 20241001214356](https://github.com/user-attachments/assets/2edb4f72-22f3-406b-813d-29fd62832f25)

Vuelvo a realizar un escaneo de directorios pero esta vez a partir de la dirección `http://172.17.0.2/wordpress/`.

![Pasted image 20241001214614](https://github.com/user-attachments/assets/4abbef05-a468-4f26-965b-e681b11df8bb)

En la web `http://172.17.0.2/wordpress/` encuentro un usuario `chocolate` que ha posteado algo.

![Pasted image 20241001214623](https://github.com/user-attachments/assets/5e6e8647-4de8-46d5-ac23-00b261158971)

No puedo acceder a ninguna de las direcciones encontradas por lo que voy a realizar fuerza bruta al ssh con el usuario que he obtenido (Si añado la ip de la máquina víctima al `/etc/hosts` y le asigno el nombre `collections.dl`, puedo acceder a un panel de login de wordpress, pero es más rápido y fácil de la siguiente forma.).

![Pasted image 20241001215024](https://github.com/user-attachments/assets/c13ebdb9-602e-4d29-9cfc-0737a8d815bc)

![Pasted image 20241001215059](https://github.com/user-attachments/assets/1482db98-0c8f-4639-b990-26e7d271f96b)

Consigo acceso pero no puedo escalar privilegios.

Decido entonces conectarme a su base de datos mongodb en el puerto 27017.

![Pasted image 20241001220231](https://github.com/user-attachments/assets/a32acc1b-0b92-43b8-95df-0598b7e4e6ec)

Encuentro el usuario `dbadmin` y su password `chocolaterequetebueno123`.

Inicio sesión con esas credenciales.

![Pasted image 20241001220334](https://github.com/user-attachments/assets/b2994e07-fab8-4585-9503-03fffafdf03e)

No encuentro la forma de escalar privilegios de nuevo, por lo que pruebo a intentar iniciar sesión como root con las contraseñas que he obtenido hasta ahora y consigo ser root con la password `chocolaterequetebueno123`.

![Pasted image 20241001220658](https://github.com/user-attachments/assets/dcbd8e0a-1873-4243-9655-9085842c2a2c)
