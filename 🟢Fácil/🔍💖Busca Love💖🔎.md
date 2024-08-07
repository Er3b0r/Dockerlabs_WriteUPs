
Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240806135550](https://github.com/user-attachments/assets/177f98c5-81c1-48d8-81cc-158bf65b31bc)

Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.

![Pasted image 20240806135949](https://github.com/user-attachments/assets/20d5dbcc-3dda-49c1-bf71-eb0d3831ed32)

Accedo a la dirección encontrada.

![Pasted image 20240806140024](https://github.com/user-attachments/assets/55289c61-3364-4212-b282-7ea1086c6dce)

Los enlaces no me llevan a ningún otra dirección.

Si inspecciono el código fuente, veo que hay un mensaje comentado.

![Pasted image 20240806141048](https://github.com/user-attachments/assets/acd627af-7263-4585-994f-78e4668dba01)

Se me ocurre probar a utilizar la herramienta de wfuzz para ver si la web es vulnerable a un LFI (Local File Inclusion).

Con el siguiente comando intento adivinar cual es el parámetro que necesito utilizar en caso de que sea vulnerable y que liste por ejemplo el archivo donde se encuentran los usuarios.

```bash
wfuzz --hc 404 --hw 115 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u 172.18.0.2/wordpress/index.php'?'FUZZ=../../../../../../../../../../etc/passwd
```
![Pasted image 20240806141908](https://github.com/user-attachments/assets/f9fc7fa5-0da0-494c-9d9b-45539b3d158f)

Ahora con el parámetro love voy a probar a introducir el siguiente contenido en la url de la web.

```bash
http://172.18.0.2/wordpress/index.php?love=../../../../../../../../../../etc/passwd
```
![Pasted image 20240806142120](https://github.com/user-attachments/assets/73fbeadb-c693-44c2-b12c-63d012428c1d)

Consigo obtener el archivo de la máquina que almacena los usuarios.

Ahora voy a realizar un ataque de fuerza bruta con hydra con los usuarios pedro y rosa.

Para el usuario Pedro no encuentro ninguna contraseña, pero para rosa sí.

![Pasted image 20240806144351](https://github.com/user-attachments/assets/2505071e-1ffc-4e2d-8200-2916ead8e1f1)

Procedo a iniciar sesión por ssh.

![Pasted image 20240806144413](https://github.com/user-attachments/assets/99f4249d-34a2-4d6e-8341-f03ec679dfd5)

Voy a intentar escalar privilegios utilizando algún binario que pueda ejecutar como sudo.

![Pasted image 20240806144657](https://github.com/user-attachments/assets/60d73e61-3a55-452e-a73c-971a945dce37)

Encuentro un código que parece estar cifrado en hexadecimal.

Voy a descifrarlo con la herramienta online [Rapid Tables](https://www.rapidtables.com/convert/number/hex-to-ascii.html).

![Pasted image 20240806144922](https://github.com/user-attachments/assets/77d4046b-d22b-4947-8708-964760ca497a)

Pruebo a intentar iniciar sesión como pedro o como root pero la contraseña parece no ser esa, por lo que igual está cifrada.

Al final parece que está cifrada en Base32.

![Pasted image 20240806145310](https://github.com/user-attachments/assets/f2e62bcb-ced0-4642-886d-89eeb191071c)

Inicio sesión como pedro y compruebo los binarios para poder escalar privilegios.

![Pasted image 20240806145429](https://github.com/user-attachments/assets/7e88fb06-45eb-4c49-8d14-0d2fdd0124cb)

Con la herramienta online [GTFOBins](https://gtfobins.github.io/gtfobins/env/#sudo), introduzco el siguiente comando y consigo ser root.

![Pasted image 20240806145610](https://github.com/user-attachments/assets/3521626c-ab54-4338-8350-1e2c0afdb3b4)
