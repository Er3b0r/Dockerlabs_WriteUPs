Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240929170245](https://github.com/user-attachments/assets/077d04d4-9e0a-44da-8e6e-1c27e00e4a53)

Accedo al recurso web del puerto 80 y veo la siguiente web.

![Pasted image 20240929170710](https://github.com/user-attachments/assets/31561319-9076-4096-9732-6e16c8885937)

A primera vista no veo nada por lo que procedo a hacer un escaneo de directorios con gobuster.

![Pasted image 20240929172133](https://github.com/user-attachments/assets/307e1e7a-b221-4f7b-ac02-ec8672c7c41f)

Encuentro un directorio llamado `whoami` en el que no hay nada.

![Pasted image 20240929172149](https://github.com/user-attachments/assets/6ab3ff5f-6628-485c-92e9-8ce2234587ed)

Mirando el código fuente de la web principal, encuentro que hay un recurso llamado script.js.
Si accedo al recurso veo que en el código hay el siguiente mensaje.

![Pasted image 20240929172305](https://github.com/user-attachments/assets/5f5889ab-332d-4128-a8cc-86c1bd88c441)

A través del navegador accedo a la siguiente ruta y encuentro un usuario y una password.

![Pasted image 20240929173044](https://github.com/user-attachments/assets/c099900a-194d-4d0f-8318-77b8a68f682d)

Accedo a la máquina a través de ssh con las credenciales que acabo de obtener.

![Pasted image 20240929173234](https://github.com/user-attachments/assets/d6110f53-aa70-4756-bf31-7966766c8599)

Ahora voy a intentar escalar privilegios.
Veo que puedo ejecutar archivos php como el usuario `chocolate` por lo que me creo un script en php que me proporcione una reverse shell, que al ejecutarse como chocolate me proporcione una consola en otro terminal de mi máquina atacante.

![Pasted image 20240929173757](https://github.com/user-attachments/assets/3528dc6a-ea4f-436d-9e17-6a240d58b3da)

![Pasted image 20240929173925](https://github.com/user-attachments/assets/a0acf05e-eba9-4737-add2-561a721f0637)

Ahora hago un tratamiento de la TTY.

```bash
script /dev/null -c bash
Control + z
stty raw -echo;fg
reset xterm
export TERM=xterm
export SHELL=bash
```

Voy a intentar escalar privilegios a root.

De primeras no encuentro nada que me ayude a escalar privilegios.

Utilizo la herramienta pspy para ver si hay algún proceso o comando que se esté ejecutando.

Descargo la herramienta y la ejecuto.

```bash
cd /home/chocolate
wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.1/pspy64
chmod +x pspy64
./pspy64
```

Encuentro que root está ejecutando el script que se encuentra en `/opt/script.php`

![Pasted image 20240930210015](https://github.com/user-attachments/assets/7d10e1a2-1af9-4bc8-9166-dca8eedf3e30)

Decido modificarlo ya que el usuario chocolate tiene los permisos para hacerlo.

Cambio el contenido por una reverse shell.

![Pasted image 20240930205935](https://github.com/user-attachments/assets/3b5016d4-609a-4485-a98c-e87090e07ea3)
