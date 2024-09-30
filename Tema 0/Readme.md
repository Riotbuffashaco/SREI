# SREI 

## Tema 0: Introducción

### Server HTTPs

***Actividad 0.1 - HTTP Introduction***
https://www.youtube.com/watch?v=eesqK59rhGA
https://www.youtube.com/watch?v=DuSURHrZG6I

**¿Quién, dónde y cuándo se crea el primer servidor web?**

Tim Berners Lee, en el cern, en 1990

**¿Cuál es la pila de protocolos usados por http?**
	
HTTP, TCP, IP

**¿Componentes de una URL?**
	
Protocolo
Anfitrión
Puerto red
Ruta

**¿Pasos en la recuperación de una página web mediante HTTP?**

1º con el comande GET

2º observamos el codigo que da

Diferencia entre páginas dinámicas y estáticas

Las estáticas son archivos html puros, mientras que las dinámicas presentan comandos de actualización de la pagina
 
**¿Cómo usar telnet para acceder a un servidor web?**
(solución en actividad 0.3)
Request. Métodos principales

GET 
POST
HEAD
	

***Actividad 0.2 - UDP and TCP: Comparison of Transport Protocols***
https://www.youtube.com/watch?v=Vdc8TCESIg8

**Diferencias entre udp y tcp?**

TCP es un protocolo confiable que garantiza la entrega de los datos en el orden
correcto, pero es más lento. UDP es más rápido, pero no asegura la entrega ni el orden de los datos, ideal para aplicaciones en tiempo real.

**¿Qué aplicaciones usan tcp?**

Navegadores web
Correo electrónico
Transferencia de archivos
Mensajería instantánea y redes sociales
Conexiones remotas

**¿Qué aplicaciones usan udp?**

Streaming de video y audio en tiempo real (YouTube, Netflix, Twitch, etc.)
Videojuegos en línea (como Fortnite, PUBG, etc.)
VoIP (Voz sobre IP) (como Skype, Zoom, WhatsApp)
DNS (Sistema de nombres de dominio) para consultas rápidas.
Protocolos de transmisión en red como SNMP (para monitorear redes) y DHCP.

**¿Qué capa almacena el puerto?**

La capa de transporte

**¿Qué capa almacena la dirección IP?**

La capa de red

**¿Qué es three-way handshake?**

Es un proceso para establecer una conexion entre cliente y servidor. 

Tiene 3 pasos:
SYN: El cliente envía un mensaje SYN (synchronize) al servidor para iniciar la conexión.
SYN-ACK: El servidor responde con un SYN-ACK (synchronize acknowledgment) para reconocer la solicitud.
ACK: El cliente envía un ACK (acknowledgment) al servidor confirmando la respuesta.



***Actividad 0.3 - Práctica telnet/http***
https://www.youtube.com/watch?v=xpBpGC08f4Q&t=189s

**Lee el artículo y prueba los ejemplos sugeridos en él.**

Nota: Si usamos Windows 10, tenemos que activar “telnet”
http://www.lawebdelprogramador.com/foros/Windows-10/1510815-Como-activar-Telnet-en-Windows-10.html


Activamos Telnet en las caracteristicas de Windows:

![imagen](https://github.com/user-attachments/assets/dbf53ac3-845a-426f-baec-f1c42a530391)


Con el comando telnet google.com 80 nos conectamos 

![imagen](https://github.com/user-attachments/assets/ee859972-aa5f-4b9c-a445-1f16486765d4)


y escribimos GET para obtener la información

![imagen](https://github.com/user-attachments/assets/c54d79ee-e139-436b-b28a-8c834f20e69b)


***Actividad 0.4 - Usando cUrl***
https://curl.se/docs/manual.html

**Busca información sobre el comando curl y muestra al menos cinco ejemplos de uso**

cUrl es una herramienta de línea de comandos utilizada para transferir datos desde o hacia un servidor mediante varios protocolos

Realizar una petición HTTP simple

Guardar el contenido de una URL en un archivo

Descargar un archivo y renombrarlo

Enviar datos a través de una petición POST

Enviar una petición con cabeceras específicas


***Actividad 0.5 - Práctica servidor web***

Visita los siguientes enlaces:

Simple web server (ejemplo 1)
https://docs.python.org/3/library/http.server.html

HTTP server (ejemplo 2)
https://github.com/python/cpython/blob/main/Lib/http/server.py

Dummy web server (ejemplo 3)
https://gist.github.com/kabinpokhrel/6fd1275603e9d5f1e284be717cbd1bff

[PASOS]

Instala Python.

Ejecuta los ejemplos mostrados con anterioridad.

Publica en GitHub los ejemplos llevados a cabo. Los ejemplos se acompañaran con capturas de pantalla en las que se muestre su funcionamiento.

---

1 Simple web server 

CON EL CODIGO *python -m http.server 8000* LO INTRODUCIMOS EN LA CMD Y OBSERVAMOS COMO SE CREA EL SERVIDOR EN EL PUERTO 8000.

![imagen](https://github.com/user-attachments/assets/a883ed1b-282d-45e0-91e3-241cc46518a5)

---

2 HTTP server

---

3 CREAMOS UN DOCUMENTO PYTHON CON EL SIGUIENTE CODIGO:


``` python
import http.server as httpserver
import socketserver

def main(port=None):
	if port is None:
		port = 8000
	handler = httpserver.SimpleHTTPRequestHandler
	try:
		httpd = socketserver.TCPServer(("", port), handler)
		print("serving at port", port)
		httpd.serve_forever()
	except OSError:
		print("Given PORT:{} is unavailable.Try running with diffrent PORT Number!".format(port))

if __name__ == '__main__':
	main()
```
![imagen](https://github.com/user-attachments/assets/62d594fb-eec5-4fe2-858a-9c0e9a896b3b)

LO ABRIMOS DESDE LA CMD Y OBSERVAMOS COMO SE CREA EL SERVIDOR

![imagen](https://github.com/user-attachments/assets/f78db4d0-9f24-454b-b198-681439deab7f)

---

