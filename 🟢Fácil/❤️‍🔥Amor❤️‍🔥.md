Lo primero es hacer un escaneo de puertos y servicios con nmap.

![captura_1720276152](https://github.com/user-attachments/assets/c2b5a9f4-eabe-4f33-b015-560a5e8c33bc)

Vemos que reporta un servicio de apache en el puerto 80 y un ssh en el puerto 22.

Si accedemos a la dirección de apache mediante un navegador veremos lo siguiente.

![captura_1720277537](https://github.com/user-attachments/assets/edcdad1c-7ec6-48b3-9160-409644587db1)

Se menciona dos usuarios Juan y Carlota.

Supongamos que Juan al ser despedido ya no se encuentra como usuario, asique realizaremos un ataque de fuerza bruta al servicio ssh con la herramienta de Hydra para intentar obtener la contraseña de Carlota.

![captura_1720277604](https://github.com/user-attachments/assets/94404f08-b088-4d05-93bb-feb1aa65e2d2)

Hydra reporta la contraseña de carlota, por lo que ahora intento acceder via ssh con esas credenciales.

![captura_1720277679](https://github.com/user-attachments/assets/e5024882-da3a-4293-8c75-235db8dc7731)

Una vez accedo, voy a comprobar el contenido al que tengo acceso para ver que encuentro y ver si podemos escalar privilegios.

Antes de nada, voy a hacer un tratamiento de la consola para que sea más comodo utilizarla.

```bash
script /dev/null -c bash
export TERM=xterm
export SHELL=bash
```

Encuentro una imagen, la cual voy a intentar descargar en mi equipo local.

![captura_1720277864](https://github.com/user-attachments/assets/eebf6ca3-fbf4-4185-b38c-b3d5c932cc4e)

Para descargar la imagen a traves de ssh, voy a utilizar scp de la siguiente forma:

```bash
scp carlota@172.17.0.2:/home/carlota/Desktop/fotos/vacaciones/imagen.jpg ~/Mi/Ruta/
```

![captura_1720277948](https://github.com/user-attachments/assets/9289d08a-427f-4d4e-970c-6ec99c7ad38b)

Una vez descargada la imagen, voy a utilizar la herramienta steghide para comprobar si hay algun tipo de contenido oculto, en caso de obtenerlo, lo voy a almacenar en un archivo llamado secret.txt.

![captura_1720278171](https://github.com/user-attachments/assets/debf79e1-3d28-4392-8ff8-4e50c6c25639)

Muestro el contenido del archivo y veo que es un coddigo cifrado en base64.

Voy a intentar obtener el resultado de dos formas, una es utilizando una herramienta online y la otra mediante la terminal.
#### [Herramienta Online](https://www.base64decode.org/es/)

![captura_1720278309](https://github.com/user-attachments/assets/230dc3db-3534-46bf-a953-e69d36a3377f)
#### Terminal

![captura_1720278357](https://github.com/user-attachments/assets/e8b594b7-56ed-42c9-af3d-725f3cbaea4e)

Obtengo un codigo el cual podría ser una contraseña.

Siendo Carlota, listo los usuarios dentro del direcotrio home.

![captura_1720278492](https://github.com/user-attachments/assets/764c04f9-16cb-4365-9cf0-9b59a4e6c703)

Hay dos usuarios más, asique voy a probar iniciando sesión como oscar indicando la contraseña que he obtenido antes.

![captura_1720278582](https://github.com/user-attachments/assets/d8d9bf1c-2ee4-487c-a6ae-770ad3e68e54)

Una vez soy oscar, hago lo mismo que hice con carlota, listar el contenido disponible.

Encuentro un .txt, muestro el contenido y nos dice que root tiene algo en su Desktop.

Voy a intentar escalar privilegios siendo oscar, para ello hago un sudo -l.

![captura_1720278645](https://github.com/user-attachments/assets/2fe891e4-5322-4ff4-96a7-dc7e27df62f3)

Veo que tenemos permiso para ejecutar como root sin necesidad de password en el directorio /usr/bin/ruby.

Voy a utilizar la herramienta online [GTFobins](https://gtfobins.github.io/gtfobins/ruby/#sudo) filtrando por ruby y queremos utilizar sudo, asique ejecutamos el siguiente comando.

```bash
sudo /usr/bin/ruby -e 'exec "/bin/sh"'
```

Recordar que es importante indicar la ruta absoluta del archivo que podemos ejecutar como sudo sin indicar password.

![captura_1720278767](https://github.com/user-attachments/assets/99c876c9-6a18-4168-8929-e67c94ebc7bc)
