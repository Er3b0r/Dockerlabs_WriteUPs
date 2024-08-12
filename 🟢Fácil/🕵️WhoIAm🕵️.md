Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240812001812](https://github.com/user-attachments/assets/a249e96e-c020-4b09-9b03-b99088be13a2)

Accedo a la web.

![Pasted image 20240812001852](https://github.com/user-attachments/assets/cc254e3b-3205-4247-8fae-972096af347a)

Hago fuzzing web con gobuster.

![Pasted image 20240812002256](https://github.com/user-attachments/assets/9a0e4421-f021-495b-bc9d-273bae99775e)

Si accedo a la dirección /wp-admin/ encuentro un panel de login de WordPress.

![Pasted image 20240812002307](https://github.com/user-attachments/assets/6d889e64-6b22-45c1-9338-c765816278f4)

Como no tengo como iniciar sesión, voy a seguir buscando.

En la dirección /backups/, encuentro un archivo zip que procedo a descargar para ver su contenido.

![Pasted image 20240812002546](https://github.com/user-attachments/assets/f6d9a3f8-9f01-472e-acb5-0c751cb2d97f)

Descargo el archivo, lo descomprimo y veo su contenido.

![Pasted image 20240812002654](https://github.com/user-attachments/assets/f6d6e97b-bb67-439b-93e6-067073d7a76b)

Ahora ya tenemos el usuario y la contraseña para iniciar sesión en wordpress.

![Pasted image 20240812002812](https://github.com/user-attachments/assets/f2099764-e4cf-4bf6-bfbc-4dd61077ad28)

Voy a intentar buscar vulnerabilidades de los plugins que posea este wordpress, para ello primero debo saber qué plugins tiene.

![Pasted image 20240812005442](https://github.com/user-attachments/assets/82cf36da-063b-4808-935a-f1de53f1b27f)

Encuentro el siguiente plugin.

![Pasted image 20240812005522](https://github.com/user-attachments/assets/ccb9d3c8-535f-44d4-a181-6103c50e994f)

Lo siguiente es buscar algún exploit con searchsploit.

![Pasted image 20240812005614](https://github.com/user-attachments/assets/3577db83-1462-411f-a09b-46edd98b4306)

Descargo el exploit.

![Pasted image 20240812005740](https://github.com/user-attachments/assets/365b6335-2bbd-4aa2-9aef-725e7614d526)

Ejecuto el siguiente comando para crear una shell en el navegador.

![Pasted image 20240812010609](https://github.com/user-attachments/assets/316d3af8-d448-47d2-8392-763e73d0f1de)

Si ahora accedo a la URL que indica veo lo siguiente.

![Pasted image 20240812010638](https://github.com/user-attachments/assets/0e27aaf2-c68c-49e8-9d4b-5860b594ef08)

Me envío una reverse shell.

![Pasted image 20240812012330](https://github.com/user-attachments/assets/e4b56e7c-37dd-4517-be37-c72fe3711947)

Ahora tengo que intentar escalar privilegios, esto lo voy a intentar con los binarios del sistema.

![Pasted image 20240812012730](https://github.com/user-attachments/assets/bc43d8fa-4ead-4412-8672-c68aea8fe2e3)

Sigo intentando escalar privilegios.

![Pasted image 20240812012925](https://github.com/user-attachments/assets/d66e3671-1398-49c5-a29f-4294d7abe3e2)

Ahora voy a intentar ganar acceso a root con ayuda de los binarios.

Veo que puedo ejecutar un script.

```bash
#!/bin/bash
read -rp "Enter guess: " num

if [[ $num -eq 42 ]]
then
  echo "Correct"
else
  echo "Wrong"
fi
```

Ese script me devuelve correcto si el número que aporto es 42, por lo que se me ocurre ejecutar el siguiente script, que lo que hace es dar permisos SUID a la ruta /bin/bash, este valor se lo asigna a la variable prueba y le sumamos el numero 42 para que no de error.

```bash
prueba[$(chmod u+s /bin/bash >&2)]+42
```

De esta manera puedo ahora ejecutar el comando bash -p que me proporciona una bash como root.

![Pasted image 20240812014749](https://github.com/user-attachments/assets/28e4c575-31b9-4f4e-bad7-75a0af09b0f3)
