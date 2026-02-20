> # Diario de la Unidad Didáctica 5: FileZilla

> ## Qué he aprendido

En esta unidad he aprendido a montar un servidor de transferencia de archivos desde cero con FileZilla Server. He descubierto cómo gestionar accesos creando grupos y usuarios específicos, y la diferencia entre dar permisos de solo lectura o escritura.
También he aprendido cosas clave sobre redes y seguridad: cómo funciona el Modo Pasivo para no tener problemas con los routers, cómo abrir los puertos en el Firewall de Windows, y lo más importante, cómo cifrar las transferencias generando un certificado TLS para usar FTPS en lugar de FTP en texto plano.

> ## Qué no entiendo

Me sigue pareciendo un poco confuso el tema de los rangos de puertos dinámicos en el Modo Pasivo y por qué a veces el router o el firewall los bloquean si no los especificas a mano. También me cuesta un poco entender a fondo todos los parámetros técnicos a la hora de generar un certificado de seguridad (como los tipos de llaves o el fingerprint).

> ## Qué me ha gustado

Me ha gustado mucho la práctica final donde conectamos FileZilla con Apache (XAMPP). Fue muy satisfactorio subir un archivo `index.html` por el cliente FTP y ver cómo se actualizaba la página web al instante en el navegador. También mola ver el "candado" de seguridad en el FileZilla Client confirmando que la conexión está cifrada.

> ## Qué no me ha gustado

Pelearme con el error `550 Permission denied`. A veces crees que lo tienes todo bien configurado y el servidor te rechaza la subida del archivo porque se te olvidó marcar la casilla de "Write" en los permisos del grupo. También vi que intentar usar el navegador como cliente FTP hoy en día es una pérdida de tiempo por los bloqueos de seguridad.

> ## Conclusión

Esta unidad me ha servido para darme cuenta de que subir archivos a un servidor no es solo "arrastrar y soltar". Hay que pensar en la seguridad, en quién tiene acceso a qué carpeta, y en que los datos viajen cifrados. Ahora me siento capaz de gestionar las carpetas de un servidor web real de forma profesional.
