>Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240626141157](https://github.com/user-attachments/assets/d2b29fb2-03b2-41e9-92ce-e3eb47feb46a)
>Realizo un escaneo de directorios utilizando la herramienta dirb indicando la url que deseo escanear.

![Pasted image 20240626141831](https://github.com/user-attachments/assets/fa8b6771-803e-427d-afda-6e6da8106547)
>Encuentro que se trata de una página que utiliza el gestor de contenido (CMS) wordpress.

![Pasted image 20240626141800](https://github.com/user-attachments/assets/5f6dc7af-6b9f-4e71-8a63-9aef3d949535)
>Voy a la dirección de index.php en la página-ejemplo y encuentro un enlace.

![Pasted image 20240626142158](https://github.com/user-attachments/assets/f885e0aa-ed29-45a3-a3ee-37a8413329d4)
>El enlace me redirige a un login para poder acceder a wordpress.

![Pasted image 20240626142214](https://github.com/user-attachments/assets/75026661-ec04-4f28-9945-7cf2a293cbab)
>Como no tengo ninguna credencial para poder iniciar sesión, sigo buscando en la web y encuentro un enlace a una sección de comentarios.

![Pasted image 20240626145058](https://github.com/user-attachments/assets/9c296ee9-fc09-4796-bb86-50137393e281)
>En la siguiente imagen veo que un usuario llamado **mario** ha realizado un comentario, por lo que ese usuario puede que existe en alguna base de datos y pueda intentar entrar por ahi.

![Pasted image 20240626145044](https://github.com/user-attachments/assets/0526b373-8e15-43f5-983b-4cba7060231c)
>Si ahora vuelvo al panel de login de wordpress, e intento iniciar con el usuario mario veo que dicho usuario si existe pero que la contraseña que he introducido no se corresponde.

![Pasted image 20240626145412](https://github.com/user-attachments/assets/638f0509-4ffc-4192-bef1-4dd6372185f8)
>Voy a utilizar la herramienta **wpscan** para primero ver si puedo obtener algunos usuarios de wordpress.
```bash
wpscan --url http://172.17.0.2/wordpress/ --enumerate u
```

![Pasted image 20240626150711](https://github.com/user-attachments/assets/d8d54cdc-ae06-48ba-a19b-79ae7f8b27ba)
>Ahora intentaré hacer fuerza bruta a ese usuario.
```bash
sudo wpscan --url http://172.17.0.2/wordpress/ -U mario -P /usr/share/wordlists/rockyou.txt
```

![Pasted image 20240626150842](https://github.com/user-attachments/assets/51276dfd-aeee-4c74-ab94-fa57d3e9d556)
>Introduzco la clave en el login de wordpress y consigo acceso.

![Pasted image 20240626150943](https://github.com/user-attachments/assets/d5dae78b-02f1-48ff-ab2d-5eb1e194c6d8)
>Resulta que este usuario es un usuario administrador.
>Voy a intentar crear una **reverse shell** modificando el código de algunas de las páginas web disponibles.

![Pasted image 20240626151555](https://github.com/user-attachments/assets/7301f608-338d-4a33-9cf9-285e80b43a11)
>Gracias a la herramienta Reverse Shell Generator, copio el script que me permitirá generar la reverse shell y modificando ciertos parámetros ganar acceso a la máquina.

![Pasted image 20240626190831](https://github.com/user-attachments/assets/907fee45-a857-43d8-abb8-d25a8cbeaead)
>Una vez copiado el script, pego el contenido en la página twentytwentytwo/index.php.

![Pasted image 20240626190811](https://github.com/user-attachments/assets/5b366d90-4b7f-40c2-9ed4-8ab4bdc1b307)
>Si ahora accedo a la siguiente url, se me debería de generar la reverse shell, pero antes debo ponerme en escucha a traves del puerto adecuado.

![Pasted image 20240626191023](https://github.com/user-attachments/assets/61440cdd-469f-4073-b1ee-aaf6a5848daf)
>Me pongo en escucha utilizando netcat y ahora accedo a la url.

![Pasted image 20240626191057](https://github.com/user-attachments/assets/d19007d0-1e4b-4886-bbae-6da8fb8a1e98)
>Se me proporciona la reverse shell y gano acceso a la máquina víctima.

![Pasted image 20240626191914](https://github.com/user-attachments/assets/377e06dc-cc11-4f87-8b31-86fee438f07d)
>Busco los binarios que poseen permisos de root y veo que puedo hacer algo con el binario /usr/bin/env.
>Utilizo la herramienta GTFObins para buscar el script que me permita generar una shell como root a través del binario /usr/bin/env.
>Una vez ejecuto el script ya he logrado escalar los privilegios y convertirme en root.

![Pasted image 20240626192528](https://github.com/user-attachments/assets/9debb392-c43c-40ae-a55b-b39edabe4ad1)
