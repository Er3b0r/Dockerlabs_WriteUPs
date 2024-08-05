Lo primero es hacer un escaneo de puertos y servicios con nmap.


![Pasted image 20240805021806](https://github.com/user-attachments/assets/a6435f11-5d63-48d8-ae68-c631e000df28)

Inicio como anonymous al servicio ftp.

Descargo el archivo.


![Pasted image 20240805022241](https://github.com/user-attachments/assets/b60dfa41-ccd3-45a4-a36b-962262dd6605)

Intento descomprimir el archivo pero tiene una password.


![Pasted image 20240805022331](https://github.com/user-attachments/assets/26749c05-0dca-4527-8e0f-7b740236aa8d)

Voy a usar John The Ripper para intentar crackear la password.


![Pasted image 20240805022732](https://github.com/user-attachments/assets/81419fdb-c5bc-44dc-bea4-c5216db24c80)

Ahora puedo descomprimir el archivo zip con la contraseña password1.


![Pasted image 20240805023114](https://github.com/user-attachments/assets/8f5a9fd7-3fc1-493c-b116-0aac831e5395)

Obtengo el archivo password.txt con un usuario y una contraseña con los que probablemente pueda iniciar sesión por ssh.


![Pasted image 20240805023209](https://github.com/user-attachments/assets/6ef51daf-dd88-40d5-81d2-c9ff072086f5)


![Pasted image 20240805023347](https://github.com/user-attachments/assets/3ba4f5a1-9e13-4343-aba8-f1549d07919a)

Ahora voy a intentar escalar privilegios.


![Pasted image 20240805024153](https://github.com/user-attachments/assets/ffcaea25-63d4-4e80-a1a6-9cdce8700e45)

Modifico el contenido de script.js con código javascript para obtener una reverse shell gracias a la herramienta online [GTFOBins](https://gtfobins.github.io/gtfobins/node/#reverse-shell).

![Pasted image 20240805024339](https://github.com/user-attachments/assets/5062e713-fd91-4900-bf22-0d435ab7320d)

Me pongo en escucha por el puerto indicado y ejecuto el script de la siguiente manera.

```bash
sudo /usr/bin/node /home/mario/script.js
```

![Pasted image 20240805024322](https://github.com/user-attachments/assets/4941c636-58a0-48b4-bb09-f04286b14146)
