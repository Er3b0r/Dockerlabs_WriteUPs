
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240715223005.png]]
>No  voy a realizar fuzzing web ya que la máquina se cae y toca reiniciarla.
>Accedo directamente al recurso web y me encuentro que es un Jenkins.
>Como no tengo ningún tipo de credencial para poder iniciar sesión, voy a buscar algún exploit buscando la versión que utiliza este Jenkins.
![[Pasted image 20240715224523.png]]
>Con la herramienta whatweb, extraigo cierta información de la web como la versión de Jenkins.
![[Pasted image 20240715224547.png]]
>Busco algún exploit que me coincida con la versión.
![[Pasted image 20240715224608.png]]
>Descargo el archivo.
![[Pasted image 20240715224643.png]]
>Ejecuto el exploit, un LFI (Local File Inclusion), permitiéndome poder leer archivos.
>Listo el contenido del archivo de los usuarios para posteriormente realizar algún ataque de fuerza bruta.
![[Pasted image 20240715224840.png]]
>Voy a utilizar la herramienta hydra para realizar un ataque de fuerza bruta al servicio ssh.
>Encuentro las credenciales del usuario bobby.
![[Pasted image 20240716010445.png]]
>Utilizo las credenciales para iniciar sesión como bobby en ssh.
![[Pasted image 20240716010625.png]]
>Una vez accedo, voy a comprobar el contenido al que tengo acceso para ver que encuentro y ver si podemos escalar privilegios.
>Puedo ejecutar python3 como el usuario punguinito.
>Con el siguiente script, consigo acceso como pinguinito.
![[Pasted image 20240716011402.png]]
>Una vez accedo, voy a comprobar el contenido al que tengo acceso para ver que encuentro y ver si podemos escalar privilegios.
>Encuentro que puedo ejecutar un script de python.
>En principio el script no me dice nada útil, por lo que voy a reemplazar su contenido.
![[Pasted image 20240716012025.png]]
>Sustituyo su contenido de la siguiente forma, de esta manera, cuando ejecute el script como sudo, ganaré acceso a través de una consola.
>Ejecuto el script y ya soy root.
![[Pasted image 20240716012036.png]]
