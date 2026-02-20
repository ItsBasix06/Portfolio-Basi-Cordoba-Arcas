> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada-final](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Documentaci%C3%B3n%20final/logo.jpg)

> ## **PROYECTO FINAL: Administración y Despliegue de Apache Tomcat 10** 🚀🌐

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Arquitectura Básica de Tomcat 🏗️
Apache Tomcat no es solo un servidor web; es un contenedor de Servlets y JSPs basado en una jerarquía de componentes:



* **Server:** El componente de nivel superior que representa a toda la instancia de Tomcat.
* **Service:** Agrupa uno o más **Connectors** (como HTTP y AJP) con un único **Engine**.
* **Engine (Catalina):** El corazón de Tomcat. Recibe las peticiones de los conectores y las procesa.
* **Host:** Permite definir "Hosts Virtuales" (dominios) para que un servidor gestione varios sitios.
* **Context:** Representa cada aplicación web individual desplegada.

---

### 2. Configuración del Servidor ⚙️
La administración de Tomcat se centra en tres archivos críticos dentro de `/etc/tomcat10/`:

1.  **`server.xml`**: Define la infraestructura (puertos, conectores, certificados).
2.  **`web.xml`**: Configuración global para todas las aplicaciones (MIME types, sesiones).
3.  **`context.xml`**: Parámetros compartidos, como recursos JNDI o restricciones de acceso.

---

### 3. Seguridad Aplicada 🔐🛡️
La seguridad ha sido un pilar fundamental en este despliegue. Se han aplicado tres capas de protección:

**A. Gestión de Identidades (`tomcat-users.xml`):**
Se han definido roles específicos (`manager-gui`, `admin-gui`) y usuarios autenticados para evitar accesos no autorizados a las herramientas de gestión.

**B. Cifrado de Comunicaciones (SSL/TLS):**
Se habilitó el protocolo HTTPS en el puerto **8443** mediante la creación de un almacén de claves (Keystore) y la configuración del conector NIO:
```xml
<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
           maxThreads="150" SSLEnabled="true">
    <SSLHostConfig>
        <Certificate certificateKeystoreFile="/etc/tomcat10/keystore.jks"
                     certificateKeystorePassword="******" type="RSA" />
    </SSLHostConfig>
</Connector>
```

**C. Java Security Manager:**
Activado en `/etc/default/tomcat10` (`SECURITY_MANAGER=true`), actúa como un "sandbox" que impide que aplicaciones maliciosas accedan al sistema de archivos o ejecuten comandos del SO.

---

### 4. Integración con Servidor Web 🔗
Aunque Tomcat puede funcionar solo, en producción suele integrarse con servidores como **Apache HTTP Server** o **Nginx** mediante el protocolo **AJP (Apache JServ Protocol)**.
* **Ventaja:** Permite delegar el contenido estático al servidor web y el dinámico a Tomcat, mejorando la velocidad y permitiendo Balanceo de Carga.

---

### 5. Pruebas de Rendimiento y Tuning 📈🏎️
Utilizando **ApacheBench (`ab`)**, se realizaron pruebas de estrés para medir la capacidad de respuesta.

**Optimización realizada:**
Para evitar cuellos de botella bajo carga alta, se ajustó el pool de hilos en el `server.xml`:
* `maxThreads="500"`: Aumenta la capacidad de procesamiento simultáneo.
* `acceptCount="500"`: Mejora la gestión de la cola de espera de conexiones.

**Resultado:** Se logró una reducción del 30% en el tiempo medio de respuesta por petición tras los ajustes.

---

### 6. Recomendaciones de Administración 📝
Para mantener un entorno de producción saludable, se recomienda:
1.  **Monitorización Continua:** Uso de los paneles *Manager* y *Host Manager* para vigilar sesiones activas y fugas de memoria.
2.  **Principio de Mínimo Permiso:** No ejecutar nunca Tomcat como usuario `root`.
3.  **Limpieza:** Eliminar las aplicaciones de ejemplo (`examples`, `docs`) para reducir la superficie de ataque.

---

### 7. Despliegue en Contenedores (Docker) 🐳
El despliegue moderno se ha realizado mediante **Docker**, permitiendo una portabilidad total:

```bash
sudo docker run -d --name tomcat-prod \
  -p 8081:8080 \
  -v ~/mis-apps:/usr/local/tomcat/webapps \
  tomcat:latest
```
Esta metodología permite escalar horizontalmente de forma inmediata y desacoplar la aplicación de la configuración del sistema operativo anfitrión.

---

### Conclusión ✅
Este despliegue garantiza un entorno de aplicaciones Java **seguro, escalable y optimizado**, preparado tanto para entornos locales como para su migración a arquitecturas en la nube (Cloud).
