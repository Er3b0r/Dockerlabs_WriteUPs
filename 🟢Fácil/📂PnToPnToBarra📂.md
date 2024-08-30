Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240828172152.png]]
Voy al recurso web del puerto 80.
![[Pasted image 20240828172255.png]]
Hago un escaneo de directorios con gobuster pero no encuentro nada.
Si hago clic en "Ejemplos de computadoras infectadas", me lleva a esta dirección y me aparece el siguiente mensaje.
![[Pasted image 20240828173143.png]]
Viendo la URL y el mensaje que muestra la web, podría ser vulnerable a un LFI, por lo que voy a tratar de listar el /etc/passwd.
![[Pasted image 20240828173406.png]]
Encuentro el usuario nico, voy a intentar mediante fuerza bruta obtener su posible password para poder acceder por ssh a la máquina.
No encuentro la password por lo que vuelvo a aprovecharme de la vulnerabilidad LFI para intentar obtener la clave id_rsa del usuario y poder acceder con ella.
![[Pasted image 20240828173850.png]]
Para poder copiarla con una mejor estructura, voy al código fuente de la web pulsando Control + u.
![[Pasted image 20240828173936.png]]
Creo un archivo llamado id_rsa y pego la clave en su interior, le asigno el permiso 600 e intento acceder con el archivo a la máquina por ssh.
![[Pasted image 20240828175228.png]]
Ahora voy a intentar escalar privilegios y ser root.
![[Pasted image 20240828175500.png]]
