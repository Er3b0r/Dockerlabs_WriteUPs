Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240812213740](https://github.com/user-attachments/assets/06ec20a5-5d0d-4a91-aefd-32ca98eae646)

Accedo al recurso http del puerto 80.

![Pasted image 20240812214748](https://github.com/user-attachments/assets/8c854c32-42a1-48d7-80cd-9bed14f3150d)

Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.

![Pasted image 20240812214215](https://github.com/user-attachments/assets/1efab5bc-c05d-4b8b-ace3-c1348a811310)

En la dirección obtenida encuentro lo siguiente.

![Pasted image 20240812214238](https://github.com/user-attachments/assets/ff73072c-01b4-4f89-a67c-52f812b60fc5)

Copiamos los nombres de los episodios en un archivo txt.

![Pasted image 20240812214634](https://github.com/user-attachments/assets/914d405f-de79-4cb9-ae26-9a97f9136689)

Tenemos 3 supuestos usuarios, Jon, Arya y Daenerys y puede que la contraseña de alguno de ellos sea uno de los nombres de los episodios.

Ahora voy a intentar sacar la contraseña de alguno de los usuarios anteriores para el servicio smb.

Utilizo crackmapexec para obtener la contraseña.

![Pasted image 20240812215240](https://github.com/user-attachments/assets/3797908e-c7ac-4d2f-aa0c-7862414c2b60)

Con smbmap voy a intentar enumerar los recursos compartidos en smb por el usuario jon.

![Pasted image 20240812215724](https://github.com/user-attachments/assets/e1f8f453-49af-47fc-9dfc-628f20a83a67)

Ahora con smbclient voy a tratar de descargar el contenido que me pueda ser útil.

Muestro el contenido del archivo que descargo.

![Pasted image 20240812220721](https://github.com/user-attachments/assets/f39f4d75-81fa-4c23-a238-2308e4d62a1e)

Me dan una contraseña cifrada en base64.

![Pasted image 20240812220808](https://github.com/user-attachments/assets/37658ec4-a5ed-4501-a25c-633ca60cb088)

Con la contraseña inicio sesión en ssh como jon.

![Pasted image 20240812220902](https://github.com/user-attachments/assets/0df08901-2b40-4607-9826-9829a41ad020)

En el directorio home veo el siguiente contenido.

![Pasted image 20240812221025](https://github.com/user-attachments/assets/023422a4-5f83-4f75-af21-efa310e76b10)

Voy a intentar escalar privilegios con ayuda de los binarios.

![Pasted image 20240812222043](https://github.com/user-attachments/assets/d500de29-ffdf-422a-bbc4-dde920c4576d)

Se me ocurre cambiar el contenido del archivo .mensaje.py, pero no tengo los permisos, por lo que con el comando mv, le cambio el nombre a mensaje.py, con echo modifico el contenido y creo un script que me 
proporciona una bash, vuelvo a nombrar el mensaje.py como .mensaje.py.

![Pasted image 20240812222309](https://github.com/user-attachments/assets/5e8bfc35-c3e5-45ed-9345-8ffa1c6fc476)

Al final me toca cambiar el contenido porque no se me añadieron bien las comillas, por lo que quedaría de la siguiente forma.

```bash
mv .mensaje.py mensaje.py
echo -e 'import os\nos.system(\"/bin/bash\")' > mensaje.py
mv mensaje.py .mensaje.py
```

Si ahora ejecuto el siguiente comando me convierto en el usuario aria.

![Pasted image 20240812222712](https://github.com/user-attachments/assets/76e041ac-0a7c-453a-a7d3-54b3d37a3690)

Intento seguir escalando privilegios con ayuda de los binarios y encuentro en el directorio /home/daenerys un archivo con el siguiente contenido.

![Pasted image 20240812223142](https://github.com/user-attachments/assets/a36aaa2b-3419-4b8a-93b9-ef63592803d7)

Con la contraseña drakaris me puedo logear como daenerys.

![Pasted image 20240812223305](https://github.com/user-attachments/assets/01805fd2-f3a6-418d-bc68-437be3c8712c)

Intento seguir escalando privilegios con ayuda de los binarios.

![Pasted image 20240812223441](https://github.com/user-attachments/assets/fe398f91-6308-47a1-b496-fdaef4c132b1)

Ahora modifico el contenido del script .shell.sh para proporcionarme una reverse shell a mi máquina atacante.

![Pasted image 20240812224220](https://github.com/user-attachments/assets/e54d35c5-373c-40ee-9ee5-6cdd8cb0a1d6)

Antes de ejecutar el comando anterior sudo, debo de ponerme en escucha.

Una vez escuchando por el puerto indicado, ejecuto el script y recibo la conexión.

![Pasted image 20240812224231](https://github.com/user-attachments/assets/8cdde1d6-b213-41d2-9d0b-19afb1c02b5f)
