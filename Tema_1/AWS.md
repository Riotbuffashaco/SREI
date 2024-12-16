

1. Instalar Apache y módulos necesarios
Primero, instala Apache y los módulos de SSL y autenticación con MySQL:
bash
Copiar código
sudo apt update
sudo apt install apache2 apache2-utils libapache2-mod-auth-mysql 

mysql-server


![image](https://github.com/user-attachments/assets/abb7f8cf-f10d-4eb7-8bec-b6385ab1df89)

2. Crear un certificado autofirmado
Genera el certificado y la clave:
bash
Copiar código
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt

Configura Apache para usar SSL:
bash
Copiar código
sudo a2enmod ssl
sudo a2ensite default-ssl.conf

Edita /etc/apache2/sites-available/default-ssl.conf para usar el certificado:
bash
Copiar código
SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key

3. Configurar autenticación con MySQL
Instala y configura el módulo mod_auth_mysql para usar la base de datos MySQL para la autenticación. Primero, asegúrate de tener una base de datos y tabla de usuarios configuradas.
Luego, edita el archivo de configuración de Apache para incluir algo como esto:
apache
Copiar código

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

5. Reiniciar Apache
Finalmente, reinicia Apache para que todos los cambios tengan efecto:
bash
Copiar código
sudo systemctl restart apache2

Con estos pasos, tendrás Apache con autenticación MySQL y un certificado SSL autofirmado en tu máquina virtual Ubuntu. Si necesitas más detalles, no dudes en preguntar.



