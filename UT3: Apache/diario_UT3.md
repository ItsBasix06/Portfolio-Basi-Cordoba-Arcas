# Diario de la Unidad Didáctica 3: Práctica Apache

## Qué he aprendido

En esta unidad me he centrado en el despliegue de aplicaciones web utilizando el servidor Apache. He aprendido todo el proceso necesario para montar un sitio web desde cero en Ubuntu Server.

Primero instalé Apache con `sudo apt install apache2` y comprobé que el servicio estuviera funcionando correctamente. También entendí la estructura básica donde se alojan los sitios web, y aprendí a crear mis propios directorios dentro de `/var/www/gci/`, además de preparar un archivo `index.html` personalizado con mi propio mensaje.

En la parte de VirtualHosts, comprendí que es necesario crear un archivo `.conf` dentro de `/etc/apache2/sites-available/` para definir el sitio. Ahí configuré el `DocumentRoot` y el `ServerName` (como `gci.example.com`) apuntando a mi carpeta.  

Después, habilité el sitio con `sudo a2ensite` y apliqué los cambios usando `systemctl reload`.  

Finalmente, aprendí a editar el archivo `/etc/hosts` para que mi propio sistema reconociera el dominio de forma local. Gracias a esto pude acceder al sitio escribiendo el nombre del dominio en lugar de la IP.

## Qué no entiendo

Aunque ya voy entendiendo cómo funciona, todavía tengo dudas sobre la diferencia exacta entre las carpetas `sites-available` y `sites-enabled`. Sé que los comandos como `a2ensite` se encargan de activar los archivos, pero me gustaría profundizar un poco más en cómo funciona este proceso internamente.

También quiero entender mejor cómo se gestionaría esto en un entorno real, donde no puedes editar el archivo `/etc/hosts` de cada cliente y necesitas un servidor DNS que resuelva los nombres de dominio de manera correcta.

## Qué es lo que más me ha gustado

Lo que más me ha gustado es poder personalizar la página web y ver cómo Apache deja de mostrar su página por defecto para mostrar la mía. Ese momento en el que aparece mi propio mensaje me resultó bastante motivador.

Otra cosa que disfruté fue resolver el fallo que tenía al principio. Al ver que el navegador no cargaba la página, fui investigando hasta darme cuenta de que faltaba modificar el archivo de hosts. Fue muy satisfactorio ver que, en cuanto lo corregí, todo empezó a funcionar.

## Lo que menos me ha gustado

Al principio fue frustrante configurar correctamente el VirtualHost y ver que la página seguía sin cargar debido al archivo de hosts. Me llevó un buen rato dar con la causa real.

Otra cosa que me resultó un poco pesada fue tener que recordar recargar Apache cada vez que hacía cualquier cambio en los archivos de configuración. Más de una vez olvidé hacer el `reload`, lo que me llevó a pensar que algo estaba mal configurado cuando no era así.

## Conclusión

Esta práctica me ha demostrado que Apache es un servidor muy robusto y que sigue una lógica muy clara. Sin embargo, también me ha quedado claro que un servidor web no es solo instalarlo y ya está, sino que requiere definir rutas, permisos, dominios y configuraciones para que todo funcione como debe. Gracias a esta unidad entiendo mucho mejor cómo se estructura y cómo se despliega realmente una aplicación web en un entorno profesional.

