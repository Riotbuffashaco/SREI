## 1. Configurar la autenticación MySQL en Apache
La autenticación MySQL te permite proteger directorios del servidor web utilizando una base de datos MySQL como backend para usuarios y contraseñas.

Paso 1: Instalar el módulo libapache2-mod-auth-mysql
```
sudo apt update
sudo apt install libapache2-mod-auth-mysql -y
```
Paso 2: Configurar la autenticación en un directorio específico
Edita el archivo de configuración del sitio en Apache:
```
sudo nano /etc/apache2/sites-available/000-default.conf
```
Dentro de la sección <VirtualHost *:80>, agrega la configuración para proteger un directorio.

Por ejemplo:
```
<Directory "/var/www/html/protegido">
    AuthType Basic
    AuthName "Área Restringida"
    AuthBasicProvider mysql
    AuthMySQLHost localhost
    AuthMySQLUser tu_usuario_mysql
    AuthMySQLPassword tu_contraseña_mysql
    AuthMySQLDB tu_base_de_datos
    AuthMySQLUserTable tu_tabla_de_usuarios
    AuthMySQLNameField nombre_de_usuario
    AuthMySQLPasswordField contraseña
    Require valid-user
</Directory>
```
Crea el directorio protegido:

```
sudo mkdir /var/www/html/protegido
echo "Este contenido está protegido" | sudo tee /var/www/html/protegido/index.html
```

Paso 3: Reiniciar Apache
Reinicia Apache para aplicar los cambios:
```
sudo systemctl restart apache2
```

## 2. Configurar un certificado SSL autofirmado
   
Paso 1: Generar el certificado autofirmado
Crea el certificado y la clave privada:

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
```

Paso 2: Configurar Apache para usar el certificado

Habilita el módulo SSL y el sitio SSL:
```
sudo a2enmod ssl
sudo a2ensite default-ssl
```

Edita el archivo de configuración del sitio SSL:

```
sudo nano /etc/apache2/sites-available/default-ssl.conf
```
Asegúrate de que las siguientes líneas apunten al certificado y clave:

```
SSLEngine on
SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
```

Reinicia Apache para activar SSL:

```
sudo systemctl restart apache2
```
Paso 3: Probar HTTPS

Accede a tu máquina virtual mediante HTTPS en el navegador:
```
https://<IP-de-la-maquina-virtual>
```

## 3. Verificar la configuración

Probar autenticación MySQL:
Accede al directorio protegido (http://<IP>/protegido) y verifica que se solicite usuario y contraseña.




