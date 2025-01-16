## Lee el artículo anterior. Instala y configura bin9 en primer lugar como servidor caché y por último como forwarding. 

En ambos casos debes:
Comprueba la sintaxis del archivo de configuración (named-checkconf)
Visualiza el archivo log y comprueba que responde adecuadamente (/var/log/syslog)
-------

**1. Instalar BIND9:**

Abre una terminal y ejecuta el siguiente comando para instalar BIND9:
```
sudo apt update
sudo apt install bind9 bind9utils bind9-doc
```
![imagen](https://github.com/user-attachments/assets/f7f72114-3d8c-4f45-8bfb-b81e7663398d)

**2. Configuración de BIND9 como Servidor Caché:**

 --> 2.1 Editar el archivo de configuración:

El archivo principal de configuración de BIND9 es /etc/bind/named.conf.options. Abre este archivo en un editor de texto:

```sudo nano /etc/bind/named.conf.options```

  --> 2.2 Configurar como servidor caché:

En la sección options, realiza las siguientes modificaciones:
```
options {
    directory "/var/cache/bind";

    // Habilitar recursividad (servidor caché)
    recursion yes;
    allow-query { any; };  // Permitir consultas desde cualquier fuente

    // Configurar los servidores raíz
    forwarders {
        8.8.8.8;  // Google DNS
        8.8.4.4;  // Google DNS
    };

    // Otras configuraciones de seguridad
    dnssec-validation auto;
};
```

![imagen](https://github.com/user-attachments/assets/68d818e6-f329-482f-b623-7ea138818e52)


Guarda los cambios y cierra el editor.

--> 2.3 Verificar la sintaxis del archivo de configuración:

Para asegurarte de que la configuración no tiene errores de sintaxis, usa el siguiente comando:

```
sudo named-checkconf
```

Si no devuelve ningún error, la configuración es válida.

--> 2.4 Reiniciar el servicio de BIND9:

Reinicia el servicio para aplicar los cambios:

```
sudo systemctl restart bind9
```

--> 2.5 Comprobar los registros en el log:

Puedes verificar que BIND9 esté funcionando correctamente mirando el archivo de log, que generalmente se encuentra en /var/log/syslog o /var/log/messages. Para ver los logs:

```
sudo tail -f /var/log/syslog
```

![imagen](https://github.com/user-attachments/assets/e472f563-9f5a-4b9a-ad36-5b4a513ff390)

Busca entradas relacionadas con BIND9 para confirmar que el servicio está funcionando como servidor caché.

**3. Configuración de BIND9 como Forwarding:**

--> 3.1 Editar el archivo de configuración para configurar el forwarding:

Si deseas que BIND9 actúe como un servidor forwarding, modifica la misma sección options en /etc/bind/named.conf.options.

```
options {
    directory "/var/cache/bind";

    // Habilitar recursividad
    recursion yes;
    allow-query { any; };

    forwarders {
        8.8.8.8;  // Google DNS
        8.8.4.4;  // Google DNS
    };

    // Otras configuraciones de seguridad
    dnssec-validation auto;
};
```

![imagen](https://github.com/user-attachments/assets/6eee748f-1d6f-48c8-bf6b-6ee5b3bef51c)

--> 3.2 Verificar y reiniciar:

Al igual que con la configuración de servidor caché, verifica la sintaxis y reinicia el servicio de BIND9:
```
sudo named-checkconf
sudo systemctl restart bind9
```
--> 3.3 Verificar en los logs:

Usa el comando para revisar el archivo /var/log/syslog y asegurarte de que todo está funcionando correctamente.
```
sudo tail -f /var/log/syslog
```
![imagen](https://github.com/user-attachments/assets/acb581b4-ae87-487f-ad95-9d87a35e0ddf)

