
---
>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.
![[Pasted image 20240620022757.png]]
>Ahora voy a explicar dos formas diferentes de resolver esta máquina, una es utilizando un exploit de metasploit y la otra es ejecutando un archivo python que obtengo con la herramienta searchsploit.
>![[Pasted image 20240620023735.png]]
## MODO 1
>Para este primer método voy a utilizar metasploit.
>Lo primero es abrir ejecutar la herramienta y buscar a ver si existe algún exploit.
![[Pasted image 20240620023750.png]]
>Encuentro uno que me va a servir para poder ganar acceso gracias al servicio ftp de la máquina.
>Lo configuro añadiendo la ip del host y el puerto.
>Una vez configurado, lanzo el exploit y ya tengo acceso como root a la máquina.
![[Pasted image 20240620023954.png]]

---

## MODO 2
>Descargo el archivo python que me proporcionó el searchsploit.
![[Pasted image 20240620025356.png]]
>Para saber que contiene el script de python, muestro su contenido por si es necesario modificar algo como por ejemplo el puerto.
![[Pasted image 20240620025427.png]]
>Una vez modificado, ejecuto el script seguido de la ip de la máquina.
>Y así consigo conectarme como root.
![[Pasted image 20240620025618.png]]
