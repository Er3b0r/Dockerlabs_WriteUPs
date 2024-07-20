
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[captura_1720276152.png]]
>Vemos que reporta un servicio de apache en el puerto 80 y un ssh en el puerto 22.
>Si accedemos a la dirección de apache mediante un navegador veremos lo siguiente.
![[captura_1720277537.png]]
>Se menciona dos usuarios Juan y Carlota.
>Supongamos que Juan al ser despedido ya no se encuentra como usuario, asique realizaremos un ataque de fuerza bruta al servicio ssh con la herramienta de Hydra para intentar obtener la contraseña de Carlota.
![[captura_1720277604.png]]
>Hydra reporta la contraseña de carlota, por lo que ahora intento acceder via ssh con esas credenciales.
![[captura_1720277679.png]]
>Una vez accedo, voy a comprobar el contenido al que tengo acceso para ver que encuentro y ver si podemos escalar privilegios.

>Antes de nada, voy a hacer un tratamiento de la consola para que sea más comodo utilizarla.
```bash
script /dev/null -c bash
export TERM=xterm
export SHELL=bash
```

>Encuentro una imagen, la cual voy a intentar descargar en mi equipo local.
![[captura_1720277864.png]]
>Para descargar la imagen a traves de ssh, voy a utilizar scp de la siguiente forma:

```bash
scp carlota@172.17.0.2:/home/carlota/Desktop/fotos/vacaciones/imagen.jpg ~/Mi/Ruta/
```

![[captura_1720277948.png]]
>Una vez descargada la imagen, voy a utilizar la herramienta steghide para comprobar si hay algun tipo de contenido oculto, en caso de obtenerlo, lo voy a almacenar en un archivo llamado secret.txt.
![[captura_1720278171.png]]
>Muestro el contenido del archivo y veo que es un coddigo cifrado en base64.
>Voy a intentar obtener el resultado de dos formas, una es utilizando una herramienta online y la otra mediante la terminal.
#### [Herramienta Online](https://www.base64decode.org/es/)
![[captura_1720278309.png]]
#### Terminal
![[captura_1720278357.png]]
>Obtengo un codigo el cual podría ser una contraseña.
>Siendo Carlota, listo los usuarios dentro del direcotrio home.
![[captura_1720278492.png]]
>Hay dos usuarios más, asique voy a probar iniciando sesión como oscar indicando la contraseña que he obtenido antes.
![[captura_1720278582.png]]
>Una vez soy oscar, hago lo mismo que hice con carlota, listar el contenido disponible.
>Encuentro un .txt, muestro el contenido y nos dice que root tiene algo en su Desktop.
>Voy a intentar escalar privilegios siendo oscar, para ello hago un sudo -l.
![[captura_1720278645.png]]
>Veo que tenemos permiso para ejecutar como root sin necesidad de password en el directorio /usr/bin/ruby.
>Voy a utilizar la herramienta online [GTFobins](https://gtfobins.github.io/gtfobins/ruby/#sudo) filtrando por ruby y queremos utilizar sudo, asique ejecutamos el siguiente comando.

```bash
sudo /usr/bin/ruby -e 'exec "/bin/sh"'
```

>Recordar que es importante indicar la ruta absoluta del archivo que podemos ejecutar como sudo sin indicar password.
![[captura_1720278767.png]]
