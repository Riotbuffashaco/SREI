# SREI 

## Tema 0: Introducción

### Server HTTPs

Actividad 0.5 - Práctica servidor web

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

