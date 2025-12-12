> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web



![img](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT3%3A%20Apache/img/HTTPS-Portada.png)




> ### U.T. 3 **Práctica 2: Apache HTTPS**

**Curso:** 2ºDAW


**Autor:** Basi Córdoba Arcas

**Fecha:** 21/11/2025


> ### 1.Investigación 🔍
> #### Funcionamiento del protocolo HTTPS y su importancia en la seguridad web. 🔒🌐

El **HTTPS** (HyperText Transfer Protocol Secure) es la versión segura del protocolo HTTP, el "idioma" base que utilizan los navegadores y servidores web para comunicarse. El HTTPS no actúa solo; utiliza un protocolo de encriptación llamado TLS (Transport Layer Security), el sucesor moderno del antiguo SSL. Se utilizan dos tipos de clave Publica y Privada.


> #### Tipos de certificados SSL/TLS 📜🔑
- `Certificados Autofirmados:` Son certificados generados y firmados por el mismo servidor o entidad que los utiliza, sin la intervención de un tercero. Es como si tú mismo te expidieras un documento de identidad; tiene tus datos, pero nadie más avala que sean reales.
  
- `Certificados de Autoridad de Certificación:` Son emitidos por organizaciones de terceros reconocidas globalmente (como DigiCert, Sectigo, o la gratuita Let's Encrypt). Estas entidades actúan como notarios digitales.
  
> #### Módulos de Apache2 necesarios para habilitar SSL/TLS en Ubuntu 🌐🔒

Para habilitar SSL/TLS en un servidor Apache2 corriendo en Ubuntu, el proceso es modular. Aunque hay un módulo indispensable. Es el modulo `ssl`. Su `funcion` es proporcionar la interfaz para la biblioteca OpenSSL, permitiendo el cifrado mediante los protocolos SSL v3 y TLS.
`Comando:` 
```bash 
sudo a2enmod ssl 
```
> #### Módulos Complementarios 🧩➕

Si bien `mod_ssl` habilita el cifrado, una configuración segura y moderna requiere gestionar redirecciones y cabeceras de seguridad. Existen modulos **Altamente Recomendados:**

`mod_rewrite` - `mod_headers` -  `mod_http2`



> ### Desarrollo 💻🦅

> 1.Instalar y verificar el estado de Apache2 en Ubuntu 📦✅

Para ello lo que tenemos que hacer antes de nada es `actualizar` los paquetes en Ubuntu:
```bash
sudo apt update
```

Una vez instalado comprobamos de que tenemos Apache2 `instalado` en el sistema y su `estado` actual del servicio:
```bash
sudo apt install apache2 && sudo systemctl status Apache2
```

![instalacion-status](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT3%3A%20Apache/img/comprobacion-y-estadp-apache2.png)

> 2.Habilitar los módulos SSL y headers 🔐📜

Para poder **habilitar** los modulos `SSL` y `headers` arriba en la investigacion puse como habilitar y teniamos que usar `a2nmod` para poder habilitar los dos modulos y luego nos pedirá reiniciar el servicio apache con `sudo systemctl restart Apache2` para que los cambios surjan:

```bash
sudo a2enmod ssl headers
```

![habilitar-modulos](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT3%3A%20Apache/img/habilitar-modulos.png)


> 3.Generar un certificado SSL/TLS 🔑📄

Con este comando voy a `generar` un certificado `Autofirmado` de 365 dias para hacer pruebas en esta practica:

![generar-certificado](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT3%3A%20Apache/img/creacion-certificado.png)



> 4.Configurar un VirtualHost para escuchar en el puerto 443 usando HTTP ⚙️🌐

 Lo primero de todo para poder hacer eso tendremos que entrar a su fichero de configuracion que Apache instala por defecto al instalar Apache, por ello ponemos el siguiente comando y accedemos:
 ```bash
sudo nano /etc/apache2/sites-available/default-ssl.conf
```

Una vez dentro del fichero buscamos unas lineas que comienzen por `SSLCertificateFile` y `SSLCertificateKeyFile`y hay que modificar su ruta y el fichero de configuracion quedaria asi:
```bash
<IfModule mod_ssl.c>
    <VirtualHost _default_:443>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        
        SSLEngine on

        # Clave Publica
        SSLCertificateFile      /etc/ssl/certs/apache-selfsigned.crt

        # Clave Privada
        SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
    </VirtualHost>
</IfModule>
```

![clave-publica-privada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT3%3A%20Apache/img/fichero-claves-publica-privada.png)


Despues de eso guardamos cambios y restablecemos con `restart` y comprobamos que todo anda bien con `status`:
```bash
usuario@usuario-VirtualBox:~$ sudo systemctl restart apache2
usuario@usuario-VirtualBox:~$ sudo systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/apache2.service; enabled; preset: enabled)
     Active: **active** (running) since Fri 2025-12-05 18:24:51 CET; 3s ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 7078 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)
   Main PID: 7081 (apache2)
      Tasks: 55 (limit: 9433)
     Memory: 6.2M (peak: 6.7M)
        CPU: 38ms
     CGroup: /system.slice/apache2.service
             ├─7081 /usr/sbin/apache2 -k start
             ├─7083 /usr/sbin/apache2 -k start
             └─7084 /usr/sbin/apache2 -k start

dic 05 18:24:51 usuario-VirtualBox systemd[1]: apache2.service: Deactivated successfully.
dic 05 18:24:51 usuario-VirtualBox apachectl[7073]: AH00558: apache2: Could not reliably determine the server's fully qualified dom>
dic 05 18:24:51 usuario-VirtualBox systemd[1]: Stopped apache2.service - The Apache HTTP Server.
dic 05 18:24:51 usuario-VirtualBox systemd[1]: Starting apache2.service - The Apache HTTP Server...
dic 05 18:24:51 usuario-VirtualBox apachectl[7080]: AH00558: apache2: Could not reliably determine the server's fully qualified dom>
dic 05 18:24:51 usuario-VirtualBox systemd[1]: Started apache2.service - The Apache HTTP Server.
```


> 5.Adaptar las directivas necesarias para redirección HTTP → HTTPS ⚙️➡️🔒

Para automatizar la seguridad y que nadie entre por error a la versión insegura de tu web, modificaremos el archivo que controla el `puerto 80 (HTTP)`, para ello nos metemos dentro del fichero de configuracion:

```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

Una vez dentro tenemos que agregar las siguientes lineas al final:

```bash
    # INICIO BLOQUE REDIRECCIÓN
    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
    # FIN BLOQUE REDIRECCIÓN
```
![https-por-defecto](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT3%3A%20Apache/img/https-por-defecto-virtual.png)



> 6.Reiniciar/recargar Apache y validar la correcta implementación mediante navegador o curl 🔄✅🌐

Antes de reiniciar, siempre comprobamos que no falte un espacio o una letra, ya que un error aquí tumbaría el servidor, usamos el siguiente comando:

```bash
sudo apache2ctl configtest
```

Y ahora una vez que diga **Syntax OK** reiniciamos y verificamos el estado con:

```bash
sudo systemctl restart apache2 && sudo systemctl status apache2
```
![status-restar-systax-ok](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT3%3A%20Apache/img/syntax-ok-restart-status.png)

Y ahora llego el momento final para saber si funciona, poner nuestra direccion IP en el navegador en mi caso es `https://172.17.0.1/` y voala,funciona correctamente:

![funcionamiento-navegador-final](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT3%3A%20Apache/img/comprobacion-funcionamiento.png)


> ### Conclusiones 🧠
He aprendido que securizar un servidor requiere precisión absoluta: no basta con instalar Apache, hay que activar manualmente módulos y sitios. La mayor lección ha sido desconfiar de los errores genéricos del navegador y confiar en la terminal; el comando `apache2ctl configtest` fue indispensable para detectar fallos de sintaxis que impedían arrancar el servicio.

> ### Dificultades encontradas ⚠️

Durante la implementación me enfrenté a varios bloqueos técnicos que tuve que ir resolviendo paso a paso. Al principio, el servidor no reconocía comandos básicos como `RewriteEngine`, lo que me obligó a investigar hasta darme cuenta de que el módulo `mod_rewrite` estaba desactivado y requería un reinicio del servicio. Posteriormente, me encontré con el error de protocolo `RX_RECORD_TOO_LONG`, causado porque el puerto 443 seguía respondiendo en HTTP plano al habérseme olvidado activar el sitio `default-ssl`.

