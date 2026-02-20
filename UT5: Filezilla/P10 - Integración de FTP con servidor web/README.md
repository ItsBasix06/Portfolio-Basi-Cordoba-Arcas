> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Integraci%C3%B3n%20de%20FTP%20con%20servidor%20web/logo.jpg)

> ### U.T. 5 **Actividad 10: Integración de FTP con servidor web 🌐🚀**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Configuración del DocumentRoot como carpeta FTP

Para integrar ambos servicios, he configurado el servidor FTP para que la carpeta raíz de un usuario sea el **DocumentRoot** del servidor web (ej. `C:\xampp\htdocs`). 

* **Configuración en FileZilla Server:** He creado un punto de montaje (Mount Point) donde la ruta virtual `/` apunta físicamente a la carpeta donde Apache busca las webs.
* **Permisos:** He asegurado que el usuario tenga permisos de **Escritura (Write)** para poder publicar cambios.

![captura-configuracion-mountpoint](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Integraci%C3%B3n%20de%20FTP%20con%20servidor%20web/mount-points-changed.png)

---

### 2. Flujo de Publicación: Subida del archivo HTML 📤

He procedido a crear un archivo llamado `index.html` en mi equipo local y lo he subido al servidor utilizando el **Modo Pasivo** y cifrado **TLS** que configuramos anteriormente.

1.  **Conexión:** Establecida mediante FileZilla Client.
2.  **Transferencia:** El log muestra el comando `STOR index.html` y la transferencia exitosa.
3.  **Seguridad:** La subida se realiza de forma cifrada, protegiendo el código fuente durante el viaje.

![captura-subida-html](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Integraci%C3%B3n%20de%20FTP%20con%20servidor%20web/subida-basi.png)

---

### 3. Verificación vía HTTP (Navegador) 🌍

Una vez subido el archivo por FTP, he abierto el navegador para comprobar que el servidor web lo sirve correctamente a través del protocolo **HTTP**.

* **URL de acceso:** `http://localhost/index.html`
* **Resultado:** A diferencia del intento fallido por protocolo FTP en la actividad anterior, aquí el navegador muestra la web perfectamente porque estamos usando el protocolo adecuado para visualización (HTTP/HTTPS).

![captura-resultado-web](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Integraci%C3%B3n%20de%20FTP%20con%20servidor%20web/comprobacion-navegador.png)

---

### 4. Descripción del Flujo Completo de Publicación

El proceso profesional de publicación web seguido ha sido:
1.  **Desarrollo Local:** El desarrollador crea la web en su PC.
2.  **Publicación (FTP):** Se usa un cliente como FileZilla para subir los archivos al servidor de forma segura (FTPS).
3.  **Despliegue:** El servidor web detecta los nuevos archivos en su `htdocs`.
4.  **Consumo (HTTP):** Los usuarios finales acceden a la web mediante su navegador sin saber que existe un FTP por detrás.
