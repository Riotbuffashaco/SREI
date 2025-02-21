
### AWS

## Introduccion

Crear la VPC:

1. Ve a la consola de AWS y entra en el servicio VPC.
2. En el menú lateral, selecciona VPC y más.
3. Asignaremos un nombre a la VPC y elige un rango de direcciones CIDR (ejemplo: 10.0.0.0/16).
4. Habilitamos DNS hostnames y resoluciones.

![imagen](https://github.com/user-attachments/assets/39f02c38-2c6a-4c38-a0cd-66dc054967c8)

Crear subredes:

1. Agregaremos dos subredes públicas (por ejemplo, 10.0.1.0/24 y 10.0.2.0/24).
2. Agregaremos dos subredes privadas (por ejemplo, 10.0.3.0/24 y 10.0.4.0/24).
3. Asigna cada subred a una zona de disponibilidad distinta para alta disponibilidad.

![imagen](https://github.com/user-attachments/assets/c81fded8-573d-4ae4-8eb1-ef45bbe968f8)


## 1. Creación de instancias

Crearemos una instancia EC2 de ubuntu con la siguiente configuracion de red y un grupo de seguridad.

Debemos asegurarnos que el puerto 80 esta abierto

![imagen](https://github.com/user-attachments/assets/81b94aa0-96a8-4658-b27d-be3454c0edd4)

## 2. Apache y PHP

Actualizaremos la Instancia con:
```
sudo apt update && sudo apt upgrade -y
```
Para instalar Apache:

```
sudo apt install apache2
```
![imagen](https://github.com/user-attachments/assets/e5e00f20-79a2-4738-a896-87d4bf7c3472)

```
sudo systemctl start apache2 (Para arrancar el servidor.)
```

```
sudo systemctl enable apache2 (para que apache inicie cada vez que arranca la instancia.)
```

![imagen](https://github.com/user-attachments/assets/e0a76f2b-4b63-467c-ad80-d46818988cce)

Para instalar php:
```
sudo apt install php8.0 libapache2-mod-php8.0 php8.0-cli php8.0-mysql -y
```

![imagen](https://github.com/user-attachments/assets/57fff505-5082-49b7-b1ba-244ed127534c)


## 3. Crear base de datos

Usaremos RDS.

Seleccionaremos MySql

![imagen](https://github.com/user-attachments/assets/a0816155-eedc-4e81-ad4c-21b7ef1b23b5)

La configuración quedará algo así:

![imagen](https://github.com/user-attachments/assets/24b6372b-35fe-4a36-a482-6880a254a046)

![imagen](https://github.com/user-attachments/assets/aec64b38-9374-4660-be6d-52469121b47e)




