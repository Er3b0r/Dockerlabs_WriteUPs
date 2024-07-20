
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240626141157.png]]
>Realizo un escaneo de directorios utilizando la herramienta dirb indicando la url que deseo escanear.
![[Pasted image 20240626141831.png]]
>Encuentro que se trata de una página que utiliza el gestor de contenido (CMS) wordpress.
![[Pasted image 20240626141800.png]]
>Voy a la dirección de index.php en la página-ejemplo y encuentro un enlace.
![[Pasted image 20240626142158.png]]
>El enlace me redirige a un login para poder acceder a wordpress.
![[Pasted image 20240626142214.png]]
>Como no tengo ninguna credencial para poder iniciar sesión, sigo buscando en la web y encuentro un enlace a una sección de comentarios.
![[Pasted image 20240626145058.png]]
>En la siguiente imagen veo que un usuario llamado **mario** ha realizado un comentario, por lo que ese usuario puede que existe en alguna base de datos y pueda intentar entrar por ahi.
![[Pasted image 20240626145044.png]]
>Si ahora vuelvo al panel de login de wordpress, e intento iniciar con el usuario mario veo que dicho usuario si existe pero que la contraseña que he introducido no se corresponde.
![[Pasted image 20240626145412.png]]
>Voy a utilizar la herramienta **wpscan** para primero ver si puedo obtener algunos usuarios de wordpress.
```bash
wpscan --url http://172.17.0.2/wordpress/ --enumerate u
```
![[Pasted image 20240626150711.png]]
>Ahora intentaré hacer fuerza bruta a ese usuario.
```bash
sudo wpscan --url http://172.17.0.2/wordpress/ -U mario -P /usr/share/wordlists/rockyou.txt
```
![[Pasted image 20240626150842.png]]
>Introduzco la clave en el login de wordpress y consigo acceso.
![[Pasted image 20240626150943.png]]
>Resulta que este usuario es un usuario administrador.
>Voy a intentar crear una **reverse shell** modificando el código de algunas de las páginas web disponibles.
![[Pasted image 20240626151555.png]]
>Gracias a la herramienta Reverse Shell Generator, copio el script que me permitirá generar la reverse shell y modificando ciertos parámetros ganar acceso a la máquina.
![[Pasted image 20240626190831.png]]
>Una vez copiado el script, pego el contenido en la página twentytwentytwo/index.php.
![[Pasted image 20240626190811.png]]
>Si ahora accedo a la siguiente url, se me debería de generar la reverse shell, pero antes debo ponerme en escucha a traves del puerto adecuado.
![[Pasted image 20240626191023.png]]
>Me pongo en escucha utilizando netcat y ahora accedo a la url.
![[Pasted image 20240626191057.png]]
>Se me proporciona la reverse shell y gano acceso a la máquina víctima.
![[Pasted image 20240626191914.png]]
>Busco los binarios que poseen permisos de root y veo que puedo hacer algo con el binario /usr/bin/env.
>Utilizo la herramienta GTFObins para buscar el script que me permita generar una shell como root a través del binario /usr/bin/env.
>Una vez ejecuto el script ya he logrado escalar los privilegios y convertirme en root.
![[Pasted image 20240626192528.png]]
