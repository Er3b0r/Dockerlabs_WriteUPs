>Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240715223005](https://github.com/user-attachments/assets/0e10fd3a-7bc3-4a4b-b2e1-96a9a9c30f4a)
>No  voy a realizar fuzzing web ya que la máquina se cae y toca reiniciarla.
>Accedo directamente al recurso web y me encuentro que es un Jenkins.
>Como no tengo ningún tipo de credencial para poder iniciar sesión, voy a buscar algún exploit buscando la versión que utiliza este Jenkins.

![Pasted image 20240715224523](https://github.com/user-attachments/assets/78de770a-c53c-4965-85d9-e6696aa1bada)
>Con la herramienta whatweb, extraigo cierta información de la web como la versión de Jenkins.

![Pasted image 20240715224547](https://github.com/user-attachments/assets/252bf319-3397-4b5a-b223-7db23b2a7382)
>Busco algún exploit que me coincida con la versión.

![Pasted image 20240715224608](https://github.com/user-attachments/assets/525650b7-c52f-4a27-8eb1-68e96e524c82)
>Descargo el archivo.

![Pasted image 20240715224643](https://github.com/user-attachments/assets/920fee09-a87c-4253-92df-f691e4513c66)
>Ejecuto el exploit, un LFI (Local File Inclusion), permitiéndome poder leer archivos.
>Listo el contenido del archivo de los usuarios para posteriormente realizar algún ataque de fuerza bruta.

![Pasted image 20240715224840](https://github.com/user-attachments/assets/c199c7c3-b272-4fed-9274-da398e4c5f00)
>Voy a utilizar la herramienta hydra para realizar un ataque de fuerza bruta al servicio ssh.
>Encuentro las credenciales del usuario bobby.

![Pasted image 20240716010445](https://github.com/user-attachments/assets/9a84ba7d-e95c-4656-bda4-d416dcd6d409)
>Utilizo las credenciales para iniciar sesión como bobby en ssh.

![Pasted image 20240716010625](https://github.com/user-attachments/assets/22f11ae4-c674-4b01-8526-4fc61e7d6770)
>Una vez accedo, voy a comprobar el contenido al que tengo acceso para ver que encuentro y ver si podemos escalar privilegios.
>Puedo ejecutar python3 como el usuario punguinito.
>Con el siguiente script, consigo acceso como pinguinito.

![Pasted image 20240716011402](https://github.com/user-attachments/assets/fa4e0507-6e37-4f8e-a1f3-f17a9774c6d5)
>Una vez accedo, voy a comprobar el contenido al que tengo acceso para ver que encuentro y ver si podemos escalar privilegios.
>Encuentro que puedo ejecutar un script de python.
>En principio el script no me dice nada útil, por lo que voy a reemplazar su contenido.

![Pasted image 20240716012025](https://github.com/user-attachments/assets/9e42dfeb-ce5b-4a3b-963e-a98ec29cf582)
>Sustituyo su contenido de la siguiente forma, de esta manera, cuando ejecute el script como sudo, ganaré acceso a través de una consola.
>Ejecuto el script y ya soy root.

![Pasted image 20240716012036](https://github.com/user-attachments/assets/5db819ab-8ae1-4106-8d1c-f728ebc49f9f)
