****Crea un script para cada uno de los siguientes problemas****

** 1.- Crea un script que añada un puerto de escucha en el fichero de configuración de Apache. El puerto se recibirá como parámetro en la llamada y se comprobará que no esté ya presente en el fichero de configuración.**

```
#!/bin/bash
Port=$1
CONF="/etc/apache2/ports.conf"
if [ -z "$Port" ]; then
  echo "Uso: $0 <Port>"
  exit 1
fi

if ! grep -q "Listen $Port" "$CONF"; then
  echo "Listen $Port" | sudo tee -a "$CONF"
  sudo systemctl restart apache2
  echo "Puerto $Port añadido y Apache reiniciado."
else
  echo "El puerto $Port ya está configurado."
fi
```


**2.- Crea un script que añada un nombre de dominio y una ip al fichero hosts. Debemos comprobar que no existe dicho dominio en el fichero hosts**
```
#!/bin/bash
DOM="$1"
IP="$2"
HOSTS_FILE="/etc/hosts"
grep -q "$DOM" "$HOSTS_FILE" || echo "$IP    $DOM" | sudo tee -a "$HOSTS_FILE" > /dev/null
```

**3.- Crea un script que nos permita crear una página web con un título, una cabecera y un mensaje**
```
#!/bin/bash
TITULO="$1"
CABECERA="$2"
MENSAJE="$3"
FICHERO_HTML="pagina_web.html"
if [ -z "$TITULO" ] || [ -z "$CABECERA" ] || [ -z "$MENSAJE" ]; then
  echo "Uso: $0 <título> <cabecera> <mensaje>"
  exit 1
fi

cat <<EOF > "$FICHERO_HTML"
<!DOCTYPE html>
<html lang="es">
<head>
    <title>$TITULO</title>
</head>
<body>
    <h1>$CABECERA</h1>
    <p>$MENSAJE</p>
</body>
</html>
EOF
echo "Página web creada: $FICHERO_HTML"
```
