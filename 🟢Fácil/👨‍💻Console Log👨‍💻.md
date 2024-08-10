Lo primero es hacer un escaneo de puertos y servicios con nmap.

![Pasted image 20240810005555](https://github.com/user-attachments/assets/77057f16-ac19-4950-978e-5bc6559fabd2)

Procedo a hacer un poco de fuzzing web con la herramienta gobuster para ver si puedo descubrir algunos directorios que a simple vista se encuentran ocultos.

![Pasted image 20240810010103](https://github.com/user-attachments/assets/914a8e85-2623-47de-8c95-2161d6195102)

Reviso el código fuente del index por si hubiese algo oculto.

![Pasted image 20240810010244](https://github.com/user-attachments/assets/07192a12-c7a6-4510-bf1b-761b91f0b6f9)

Accedo al recurso autentication.js.

![Pasted image 20240810010321](https://github.com/user-attachments/assets/7d724fed-562b-46f0-9278-5bd9b139a044)

Si ahora voy al recurso de /backend/server.js veo que la petición la tramita por post.

![Pasted image 20240810010722](https://github.com/user-attachments/assets/0878e203-bf21-407f-9670-e6da4f4bdb65)

Puedo comprobar que la contraseña es la correcta ejecutado el siguiente comando con curl.

![Pasted image 20240810011245](https://github.com/user-attachments/assets/abfc65d2-2ca4-4669-9d37-f666fff5bdd7)

Ahora voy a realizar un ataque de fuerza bruta al servicio ssh indicando el puerto 5000 ya que sino le indico por defecto utiliza el 22.

![Pasted image 20240810011534](https://github.com/user-attachments/assets/967ddd83-00a6-4952-9545-a6c7aabb836a)

Ahora inicio sesión por ssh indicando el puerto 5000 ya que sino le indico por defecto utiliza el 22.

![Pasted image 20240810011648](https://github.com/user-attachments/assets/90092fc3-96e6-4aa1-9b94-d05841ec8b98)

Voy a intentar escalar privilegios.

![Pasted image 20240810012008](https://github.com/user-attachments/assets/0f9a33d9-40fc-4c50-bf22-3ee8bbe399b1)

Dentro del editor de texto nano ejecuto lo siguiente.

```
script /dev/null -c bash
Control + R
Control + X
reset; sh 1>&0 2>&0
```

Me deja ejecutar los comandos como root dentro del editor de texto como se ve en la siguiente imagen.

![Pasted image 20240810011947](https://github.com/user-attachments/assets/b6408811-2da0-492c-99c2-19b8f641b1f1)
