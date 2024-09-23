Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240907193414](https://github.com/user-attachments/assets/ed8024e4-60da-4561-95c4-c35c69a0fc5a)

Accedo al recurso web del puerto 80.

Si hago click en el enlace 'Asucar Moreno' me lleva a otra web, pero no puedo ver su contenido porque tengo que agregarla al `/etc/hosts`.

![Pasted image 20240907193638](https://github.com/user-attachments/assets/cb1b11f6-95ce-42e1-b618-28fa0048b694)

Al parecer es la misma web.

Voy a realizar un escaneo de directorios con gobuster.

![Pasted image 20240907194118](https://github.com/user-attachments/assets/364dd085-89a1-4c89-8fb2-85799d312cb7)

Veo que la web tiene un login de Wordpress para iniciar como admin.

![Pasted image 20240907194133](https://github.com/user-attachments/assets/01740e99-5b1c-4ce0-b330-0faa12f163e9)

Ahora que se que es un WordPress voy a intentar ver qué plugins utiliza con la herramienta curl.

![Pasted image 20240907201553](https://github.com/user-attachments/assets/32eaa80f-4c9b-47e2-a8ab-163d13da9781)

Busco con searchsploit algún posible exploit que me pueda ayudar a ganar acceso a la máquina utilizando metasploit.

![Pasted image 20240907202143](https://github.com/user-attachments/assets/d13486bd-f35c-4b6a-baf8-5fc76840e99d)

Veo que puedo utilizar dos exploits, uno para realizar un LFI y otro para un CSRF.

Voy a probar con el LFI.

![Pasted image 20240907202507](https://github.com/user-attachments/assets/0d108a6e-db99-408b-9b9f-9fa7cf80764e)

Me devuelve una URL, a la que acceder y realizar el LFI.

![Pasted image 20240907202559](https://github.com/user-attachments/assets/7fb8b25b-28e0-41f6-849a-8a34065739a5)

Pego la URL cambiando el host y obtengo el archivo `/etc/passwd`.

![Pasted image 20240907202709](https://github.com/user-attachments/assets/6a932ac9-4b1d-40b0-ac02-87bae43abde7)

Ahora que tengo los usuario voy a intentar mediante fuerza bruta conseguir la password de alguno e iniciar sesión a través de ssh a la máquina víctima.

![Pasted image 20240907202924](https://github.com/user-attachments/assets/b60ff809-ad6f-499f-b3ed-945dd55680a3)

![Pasted image 20240907203005](https://github.com/user-attachments/assets/4fff022b-82ad-4ea4-84d9-34e5274524fc)

Ahora voy a intentar escalar privilegios.

![Pasted image 20240907204101](https://github.com/user-attachments/assets/3d9c2b0b-126e-4c52-aacb-f07761cf0434)

Puedo utilizar ese comando como root, por lo que se me ocurre es generar una clave RSA de 2048 bits compatible con openssh, añadirla al directorio `/.ssh/authorized_keys` para posteriormente compartir la clave con mi máquina atacante y poder iniciar sesión por ssh como root directamente.

![Pasted image 20240907204912](https://github.com/user-attachments/assets/08b854ed-b444-4f8e-b8ed-9f8699867fe2)

Como phassphrase yo he introducido admin pero sirve cualquier otra, esta clave sirve para iniciar más tarde sesión como root directamente.

Una vez hecho esto, abro otra terminal y me descargo la clave id generada y la utilizo para iniciar sesión.

![Pasted image 20240907205135](https://github.com/user-attachments/assets/203e6f59-1af9-4a2a-84fe-fba5630fabb3)
