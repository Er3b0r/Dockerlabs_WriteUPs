Lo primero es hacer un escaneo de puertos y servicios con nmap.

![captura_1720141496](https://github.com/user-attachments/assets/c9649731-4a99-45d8-9e56-47c051b349a3)

Realizo un escaneo de directorios utilizando la herramienta dirb indicando la url que deseo escanear y el puerto.

![captura_1720140089](https://github.com/user-attachments/assets/36a20841-2e3a-44f2-a62f-23891586a98c)

Si accedo al servicio http por el puerto 8080, encuentro una página tomcat, y si además intento entrar al apartado /manager, veo que es necesario iniciar sesión en un login.

![captura_1720140136](https://github.com/user-attachments/assets/e3b161df-4cc0-4065-9bf8-3153632e7662)

Como no conozco ninguna credencial, voy a acceder al servicio ftp ya que con el primer escaneo a la dirección, me reporta que puedo acceder a este servicio empleando el usuario anonymous.

![captura_1720141641](https://github.com/user-attachments/assets/26300e34-ceaf-4be9-a862-d3fb3f950165)

Una vez estoy dentro, veo que contiene un archivo llamado tomcat.txt.

Descargo el archivo y listo su contenido.

![captura_1720141681](https://github.com/user-attachments/assets/03dd5bc7-6c26-4982-869c-29439b48c37a)

El archivo no me da ningún tipo de credencial que pueda utilizar, por lo que decido buscar en la página HackTricks, credenciales por defecto del servicio tomcat.

![captura_1720190679](https://github.com/user-attachments/assets/9723f42b-c6c5-4629-bd50-37fa0e0cff09)

Pruebo las credenciales tomcat para el username y s3cr3t para la password.

![captura_1720190697](https://github.com/user-attachments/assets/8596a9ab-3624-41a5-8e36-f8983639650d)

Una vez dentro, estoy en el panel de administrador de la web. Veo que puedo subir archivos tipo WAR.

![captura_1720190717](https://github.com/user-attachments/assets/a22716c8-636d-45dc-8832-cd0548e3e06a)

Decido crear un script WAR que mediante MSFVenom, me proporcione una reverse shell.

![captura_1720191571](https://github.com/user-attachments/assets/7b7e723b-37c8-4873-a6e7-12799f77e373)

Creo el archivo WAR con los datos necesarios y le llamo shell.war.

![captura_1720191602](https://github.com/user-attachments/assets/f87399d5-46cc-4600-a5e6-2c63173ec5cb)

Subo el archivo a la web, y se crea el directorio /shell.

![captura_1720191631](https://github.com/user-attachments/assets/1c0724ab-e1d1-4678-b320-9c619f6e3f89)

Me pongo en escucha por el puerto adecuado.

Luego entro en la página donde se encuentra el archivo shell.war para que se ejecute la reverse shell.

Obtengo la reverse shell y ya soy directamente root.

![captura_1720191764](https://github.com/user-attachments/assets/e599e716-a104-497a-82d9-546e7ed9096e)
