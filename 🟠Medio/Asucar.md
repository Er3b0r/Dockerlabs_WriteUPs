Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240907193414.png]]
Accedo al recurso web del puerto 80.
Si hago click en el enlace 'Asucar Moreno' me lleva a otra web, pero no puedo ver su contenido porque tengo que agregarla al `/etc/hosts`.
![[Pasted image 20240907193638.png]]
Al parecer es la misma web.
Voy a realizar un escaneo de directorios con gobuster.
![[Pasted image 20240907194118.png]]
Veo que la web tiene un login de Wordpress para iniciar como admin.
![[Pasted image 20240907194133.png]]
Ahora que se que es un WordPress voy a intentar ver qué plugins utiliza con la herramienta curl.
![[Pasted image 20240907201553.png]]
Busco con searchsploit algún posible exploit que me pueda ayudar a ganar acceso a la máquina utilizando metasploit.
![[Pasted image 20240907202143.png]]
Veo que puedo utilizar dos exploits, uno para realizar un LFI y otro para un CSRF.
Voy a probar con el LFI.
![[Pasted image 20240907202507.png]]
Me devuelve una URL, a la que acceder y realizar el LFI.
![[Pasted image 20240907202559.png]]
Pego la URL cambiando el host y obtengo el archivo `/etc/passwd`.
![[Pasted image 20240907202709.png]]
Ahora que tengo los usuario voy a intentar mediante fuerza bruta conseguir la password de alguno e iniciar sesión a través de ssh a la máquina víctima.
![[Pasted image 20240907202924.png]]
![[Pasted image 20240907203005.png]]
Ahora voy a intentar escalar privilegios.
![[Pasted image 20240907204101.png]]
Puedo utilizar ese comando como root, por lo que se me ocurre es generar una clave RSA de 2048 bits compatible con openssh, añadirla al directorio `/.ssh/authorized_keys` para posteriormente compartir la clave con mi máquina atacante y poder iniciar sesión por ssh como root directamente.
![[Pasted image 20240907204912.png]]
Como phassphrase yo he introducido admin pero sirve cualquier otra, esta clave sirve para iniciar más tarde sesión como root directamente.
Una vez hecho esto, abro otra terminal y me descargo la clave id generada y la utilizo para iniciar sesión.
![[Pasted image 20240907205135.png]]
