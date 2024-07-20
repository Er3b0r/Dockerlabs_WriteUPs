
---
>Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[captura_1720141496.png]]
>Realizo un escaneo de directorios utilizando la herramienta dirb indicando la url que deseo escanear y el puerto.
![[captura_1720140089.png]]
>Si accedo al servicio http por el puerto 8080, encuentro una página tomcat, y si además intento entrar al apartado /manager, veo que es necesario iniciar sesión en un login.
![[captura_1720140136.png]]
>Como no conozco ninguna credencial, voy a acceder al servicio ftp ya que con el primer escaneo a la dirección, me reporta que puedo acceder a este servicio empleando el usuario anonymous.
![[captura_1720141641.png]]
>Una vez estoy dentro, veo que contiene un archivo llamado tomcat.txt.
>Descargo el archivo y listo su contenido.
![[captura_1720141681.png]]
>El archivo no me da ningún tipo de credencial que pueda utilizar, por lo que decido buscar en la página HackTricks, credenciales por defecto del servicio tomcat.
![[captura_1720190697.png]]
>Pruebo las credenciales tomcat para el username y s3cr3t para la password.
![[captura_1720190679.png]]
>Una vez dentro, estoy en el panel de administrador de la web. Veo que puedo subir archivos tipo WAR.
![[captura_1720190717.png]]
>Decido crear un script WAR que mediante MSFVenom, me proporcione una reverse shell.
![[captura_1720191571.png]]
>Creo el archivo WAR con los datos necesarios y le llamo shell.war.
![[captura_1720191602.png]]
>Subo el archivo a la web, y se crea el directorio /shell.
![[captura_1720191631.png]]
>Me pongo en escucha por el puerto adecuado.
>Luego entro en la página donde se encuentra el archivo shell.war para que se ejecute la reverse shell.
>Obtengo la reverse shell y ya soy directamente root.
![[captura_1720191764.png]]