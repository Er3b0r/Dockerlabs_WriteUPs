Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20241013174042](https://github.com/user-attachments/assets/98863cef-4f24-4293-b952-7df0d5610847)

Accedo al recurso web del puerto 80 y encuentro un formulario de login.

![Pasted image 20241013174233](https://github.com/user-attachments/assets/d1109d13-df75-40a9-9ed9-4356944448f0)

Voy a realizar un escaneo de directorios con gobuster.

Solamente encuentro el directorio `index.php` y el directorio `config.php`.

![Pasted image 20241013175221](https://github.com/user-attachments/assets/7d67eee5-e245-4996-b608-b688d623b541)

Voy a intentar hacer un bypass al formulario con un SQLi.

```sql
or 1-- -' or 1 or '1"or 1 or"
```

![Pasted image 20241013175954](https://github.com/user-attachments/assets/5f0b3d4f-5a98-4169-88b0-6903fc485346)

Encuentro al usuario `Dylan`.

![Pasted image 20241013183235](https://github.com/user-attachments/assets/9451c989-45c6-4d9a-8b2d-1a5211ae3232)

Voy a validar el usuario y ver si encuentro alguno más que pueda pertenecer al servicio SAMBA.

Voy a utilizar `enum4linux`.

```
enum4linux 172.17.0.2
```

![Pasted image 20241013183501](https://github.com/user-attachments/assets/b93d3c2f-194d-4769-a5b1-4db22edf33fc)

Encuentro los usuarios `augustus` y `bob` a parte del que ya sabía `dylan`.

Ahora con `crackmapexec` voy a intentar encontrar sus posibles contraseñas.

![Pasted image 20241013184253](https://github.com/user-attachments/assets/b675dbda-9c1a-4dc4-98fd-b802bd2c770d)

La contraseña que he encontrado ahí no parece servirme, así que voy a intentar obtener la contraseña del servicio ssh del usuario augustus.

![Pasted image 20241013184653](https://github.com/user-attachments/assets/619ac6de-942b-470f-be6b-95afc3a760d7)

Accedo al servicio ssh.

![Pasted image 20241013184726](https://github.com/user-attachments/assets/cf81e66c-19ec-4526-916b-22588aab42af)

Ahora voy a intentar escalar privilegios.

![Pasted image 20241013184954](https://github.com/user-attachments/assets/32db4f9a-1f51-4a9b-a339-9fae47197530)

Se me ocurre crear un `archivo.java` con una reverse shell y cuando lo ejecute, recibo una reverse shell que me dará acceso al usuario dylan.

Para ello voy a usar la herramienta online [revshells](https://www.revshells.com/).

![Pasted image 20241013185531](https://github.com/user-attachments/assets/c6b336b7-fd46-4a26-b4f9-e891326535be)

Ahora ejecuto el siguiente comando para ejecutar el script que me proporciona la reverse shell.

![Pasted image 20241013185613](https://github.com/user-attachments/assets/a1f364f7-e877-478b-b20b-76420e190bc2)

Hago un tratamiento de la TTY.

```bash
script /dev/null -c bash
CTRL + z
stty raw -echo;fg
reset xterm
export TERM=xterm
exprt SHELL=bash
```

Intento escalar privilegios de nuevo.

![Pasted image 20241013190545](https://github.com/user-attachments/assets/82adfdb2-e7fd-49bc-a013-5d4cde3b15d8)

![Pasted image 20241013190848](https://github.com/user-attachments/assets/44e604f2-f608-443f-9822-acfd78bd37dd)
