Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240828172152](https://github.com/user-attachments/assets/f3b67098-a81e-4d1b-8eca-062f051535f7)

Voy al recurso web del puerto 80.

![Pasted image 20240828172255](https://github.com/user-attachments/assets/4dfd8e83-441c-4ea0-94d9-1f02b6ea7ba6)

Hago un escaneo de directorios con gobuster pero no encuentro nada.

Si hago clic en "Ejemplos de computadoras infectadas", me lleva a esta dirección y me aparece el siguiente mensaje.

![Pasted image 20240828173143](https://github.com/user-attachments/assets/a6f8d42f-c6da-4d27-a483-47dc28965af0)

Viendo la URL y el mensaje que muestra la web, podría ser vulnerable a un LFI, por lo que voy a tratar de listar el /etc/passwd.

![Pasted image 20240828173406](https://github.com/user-attachments/assets/5886cfbd-36e8-46a6-891b-a878b100f92d)

Encuentro el usuario nico, voy a intentar mediante fuerza bruta obtener su posible password para poder acceder por ssh a la máquina.

No encuentro la password por lo que vuelvo a aprovecharme de la vulnerabilidad LFI para intentar obtener la clave id_rsa del usuario y poder acceder con ella.

![Pasted image 20240828173850](https://github.com/user-attachments/assets/0d294dcc-d8a9-4b64-9e44-35c510f28cd3)

Para poder copiarla con una mejor estructura, voy al código fuente de la web pulsando Control + u.

![Pasted image 20240828173936](https://github.com/user-attachments/assets/c591c167-835a-4647-a8c5-ab69d2e829cd)

Creo un archivo llamado id_rsa y pego la clave en su interior, le asigno el permiso 600 e intento acceder con el archivo a la máquina por ssh.

![Pasted image 20240828175228](https://github.com/user-attachments/assets/a122f70d-635c-4fca-9a42-9bf0b4153a17)

Ahora voy a intentar escalar privilegios y ser root.

![Pasted image 20240828175500](https://github.com/user-attachments/assets/e7b99fff-9196-4f87-ab15-39e562a85574)
