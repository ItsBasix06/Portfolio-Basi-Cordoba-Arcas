> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![img](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Configuraci%C3%B3n%20de%20seguridad%20en%20Tomcat/logo.jpg)

> ### U.T. 4 **Practica 5: Configuración de seguridad en Tomcat🛡️🔐**

**Curso:** 2ºDAW
**Autor:** Basi Córdoba Arcas
**Fecha:** 30/01/2026

> ### 1. Definir Roles y Usuarios🆔👥

Para poder entrar al panel de control, Tomcat necesita saber quién eres y qué roles tienes. Por eso, entramos a la configuración para añadir nuestro usuario administrador editando el archivo:

```bash
sudo nano /etc/tomcat10/tomcat-users.xml
```

Y ponemos las siguientes dos líneas antes de que cierre la etiqueta `</tomcat-users>`:

```xml
<role rolename="manager-gui"/>
<user username="admin" password="tu_password_seguro" roles="manager-gui"/>
```

![roles-usuarios](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Configuraci%C3%B3n%20de%20seguridad%20en%20Tomcat/roles-usuarios.png)

> ### 2. Restringir el Acceso al Manager🧱🚫

Por seguridad, Tomcat suele bloquear el acceso al Manager desde fuera de la propia máquina (localhost). En mi caso, como estoy usando una máquina virtual, para poder comunicarme con mi máquina física (Ubuntu) tengo que revisar una restricción dentro de la aplicación Manager.

Edito el archivo de contexto:

```bash
sudo nano /var/lib/tomcat10/webapps/manager/META-INF/context.xml
```

Dentro de este archivo `(context.xml)`, busco la etiqueta `<Valve>` que se encarga de filtrar las IPs. Como quiero acceder desde cualquier lugar (incluido mi ordenador anfitrión), voy a comentar esa restricción rodeándola con `` para anularla temporalmente:

![restriccion](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Configuraci%C3%B3n%20de%20seguridad%20en%20Tomcat/restriccion.png)

> ### 3. Configurar HTTPS con Keystore y Conector SSL🔐💻

El acceso por HTTP envía las contraseñas en texto plano, lo cual es inseguro. Para solucionarlo, voy a configurar un certificado autofirmado para habilitar **HTTPS** en el puerto 8443.

**3.1. Generar el almacén de claves (Keystore)**

Utilizo la herramienta `keytool` de Java para generar un certificado RSA y guardarlo en un archivo `.jks`. Para ello, ejecuto en la terminal:

```bash
sudo keytool -genkey -alias tomcat -keyalg RSA -keystore /etc/tomcat10/keystore.jks
```

A continuación, asigno los permisos correctos para que Tomcat pueda leer el archivo que acabo de crear:

```bash
sudo chown tomcat:tomcat /etc/tomcat10/keystore.jks
sudo chmod 640 /etc/tomcat10/keystore.jks
```


**3.2. Configurar el conector en server.xml**

El siguiente paso es decirle a Tomcat que use ese certificado. Edito el archivo de configuración principal:

```bash
sudo nano /etc/tomcat10/server.xml
```

Busco el conector del puerto **8443** (que por defecto viene desactivado) y lo configuro asegurándome de poner la ruta exacta de mi archivo y mi contraseña:

```xml
<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
           maxThreads="150" SSLEnabled="true">
    <SSLHostConfig>
        <Certificate certificateKeystoreFile="/etc/tomcat10/keystore.jks"
                     certificateKeystorePassword="mi_password_seguro"
                     type="RSA" />
    </SSLHostConfig>
</Connector>
```

Guardo los cambios y reinicio el servicio para aplicar la nueva configuración:

```bash
sudo systemctl restart tomcat10
```


> ### 4. Prueba de Acceso Autenticado✅🕵️

Para verificar que la seguridad está implementada, accedo desde el navegador usando el protocolo seguro HTTPS y el puerto 8443:

URL: `https://localhost:8443/manager/html`

Al ser un certificado autofirmado, el navegador me mostrará una advertencia de seguridad. Acepto el riesgo y continúo. Inmediatamente, Tomcat me solicita las credenciales. Introduzco el usuario `admin` que creé en el paso 1 y accedo con éxito al panel de control.

![navegador](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Configuraci%C3%B3n%20de%20seguridad%20en%20Tomcat/navegador-resultado.png)

> ### 5. Activar Security Manager (Opcional) 👮‍♂️🔒

Como medida extra de fortificación, Tomcat incluye un **Security Manager** de Java que limita lo que las aplicaciones web pueden hacer a nivel de sistema (leer archivos, ejecutar comandos del SO, etc.), mitigando el daño en caso de que una aplicación sea vulnerada.

Para activarlo en Ubuntu, edito el archivo de variables por defecto de Tomcat:

```bash
sudo nano /etc/default/tomcat10
```

Busco la variable `SECURITY_MANAGER` (que suele estar comentada con un `#` al principio) y la modifico para que quede activada:

```bash
SECURITY_MANAGER=yes
```

Finalmente, reinicio el servidor una última vez para que Tomcat arranque encapsulado bajo las estrictas políticas de seguridad de Java:

```bash
sudo systemctl restart tomcat10
```

![security-manager](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Configuraci%C3%B3n%20de%20seguridad%20en%20Tomcat/security-manager.png)
