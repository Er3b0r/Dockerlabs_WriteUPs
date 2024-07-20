>Lo primero es hacer un escaneo de todos los puertos para saber cuáles están disponibles y qué servicio corre en ellos.

![Pasted image 20240620022757](https://github.com/user-attachments/assets/0af6bb63-0a0b-4487-ba3f-eae76f3b72cf)
>Ahora voy a explicar dos formas diferentes de resolver esta máquina, una es utilizando un exploit de metasploit y la otra es ejecutando un archivo python que obtengo con la herramienta searchsploit.

![Pasted image 20240620023735](https://github.com/user-attachments/assets/6956afbd-e5d3-466e-8126-bc9c33b83efe)
## MODO 1
>Para este primer método voy a utilizar metasploit.
>Lo primero es abrir ejecutar la herramienta y buscar a ver si existe algún exploit.

![Pasted image 20240620023750](https://github.com/user-attachments/assets/3aec6b42-893f-4690-a03c-c58457b28906)
>Encuentro uno que me va a servir para poder ganar acceso gracias al servicio ftp de la máquina.
>Lo configuro añadiendo la ip del host y el puerto.
>Una vez configurado, lanzo el exploit y ya tengo acceso como root a la máquina.

![Pasted image 20240620023954](https://github.com/user-attachments/assets/82903afa-8c1d-4a12-a02f-738a71fa42c7)

---

## MODO 2
>Descargo el archivo python que me proporcionó el searchsploit.

![Pasted image 20240620025356](https://github.com/user-attachments/assets/114289ba-0c16-4682-9703-608aa835c29c)
>Para saber que contiene el script de python, muestro su contenido por si es necesario modificar algo como por ejemplo el puerto.

![Pasted image 20240620025427](https://github.com/user-attachments/assets/256ed84b-90e7-4156-afcb-796c1f133bce)
>Una vez modificado, ejecuto el script seguido de la ip de la máquina.
>Y así consigo conectarme como root.

![Pasted image 20240620025618](https://github.com/user-attachments/assets/1577eb54-1ee4-4873-be9c-6896bcf62df2)

