> # Diario de la Unidad Didáctica 3: Práctica Apache

> ## Qué he aprendido

En esta unidad trabajé con Apache para montar un sitio web en Ubuntu Server. Aprendí a instalar Apache (`sudo apt install apache2`), crear mis propios directorios en `/var/www/gci/` y hacer un `index.html` con un mensaje personal.

También aprendí a configurar VirtualHosts creando archivos `.conf` en `/etc/apache2/sites-available/`, definiendo `DocumentRoot` y `ServerName`, y luego habilitándolos con `a2ensite` y recargando Apache con `systemctl reload`.  

Por último, entendí cómo editar `/etc/hosts` para que mi sistema reconozca el dominio localmente y poder acceder a él usando un nombre en lugar de la IP.

> ## Qué no entiendo

Todavía me lía un poco la diferencia entre `sites-available` y `sites-enabled`, aunque sé que `a2ensite` hace la conexión entre ellos.  

También quiero aprender cómo se gestionaría esto en un servidor real, donde no puedes tocar el archivo `hosts` de todos los clientes y necesitas un servidor DNS.

> ## Qué me ha gustado

Me gustó personalizar la página y ver que Apache dejaba de mostrar la página por defecto.  
También fue muy satisfactorio arreglar el problema de que la página no cargaba, descubriendo que faltaba modificar el archivo `hosts`.

> ## Qué no me ha gustado

Al principio me frustró que el sitio no cargara a pesar de tener el VirtualHost configurado.  
Además, a veces olvidaba recargar Apache después de cambios y me costaba entender por qué no funcionaba.

> ## Conclusión

Apache es un servidor bastante sólido y lógico, pero requiere paciencia y entender bien cómo funcionan las rutas, los permisos y los dominios. Esta práctica me ayudó mucho a dar mis primeros pasos en el despliegue web y a comprender cómo funciona un servidor en la práctica.
