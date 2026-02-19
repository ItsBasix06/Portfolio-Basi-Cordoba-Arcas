> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web



![img]()



> ### U.T. 4 **Practica 5: Configuración de seguridad en Tomcat🛡️🔐**

**Curso:** 2ºDAW


**Autor:** Basi Córdoba Arcas

**Fecha:** 30/01/2026


> ### 1. Definir Roles y Usuarios🆔👥

Para poder entrar al panel de control, Tomcat necesita saber quién eres y que roles tengo,por eso entramos dentro para añadir roles con:
```bash
sudo nano /etc/tomcat10/tomcat-users.xml
```

Y ponemos las siguientes dos lineas antes de que cierre la etiqueta `</tomcat-users>`:
```bash
<role rolename="manager-gui"/>
<user username="admin" password="tu_password_seguro" roles="manager-gui"/>
```

![roles-usuarios]()


> ### 2. Restringir el Acceso al Manager🧱🚫

Por seguridad, Tomcat suele bloquear el acceso al Manager desde fuera de la propia máquina (localhost), en mi caso como estoy usando una máquina virtual, para poder comunicarme con mi maquina fisica ubuntu tengo que revisar una restriccion dentro del archivo
```bash
sudo nano /usr/share/tomcat10-admin/manager/META-INF/context.xml
```
Dentro de este archivo `(context.xml)`, busco la etiqueta <Valve> que se encarga de filtrar las IPs. Como quiero acceder desde cualquier lugar (incluido mi ordenador anfitrión), voy a comentar esa restricción para anularla temporalmente:

> ### 3. Prueba de Acceso Autenticado✅🕵️
Para verificar que la seguridad está implementada, accedo desde el navegador usando el protocolo seguro HTTPS y el puerto 8443:

URL: `https://localhost:8443/manager/html`

Al ser un certificado autofirmado, el navegador me mostrará una advertencia de seguridad. Acepto el riesgo y continúo. Inmediatamente, Tomcat me solicita las credenciales. Introduzco el usuario admin que creé en el paso 1.
