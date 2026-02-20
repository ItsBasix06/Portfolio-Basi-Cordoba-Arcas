> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20con%20clientes%20gr%C3%A1ficos/logo.jpg)

> ### U.T. 5 **Actividad 7: Pruebas con clientes gráficos 🖱️📁**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Configuración de una Conexión Guardada

Para agilizar el trabajo diario, no es eficiente introducir los datos manualmente cada vez. He configurado el **Gestor de Sitios** de FileZilla Client para guardar el perfil de nuestro servidor:
* **Nombre del sitio:** Mi Servidor Local
* **Protocolo:** FTP - Protocolo de transferencia de archivos
* **Servidor:** `127.0.0.1`
* **Cifrado:** Usar FTP explícito sobre TLS si está disponible (para mantener la seguridad configurada en la Actividad 2).
* **Modo de acceso:** Normal (con usuario y contraseña).

![captura-gestor-sitios](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20con%20clientes%20gr%C3%A1ficos/usuario1-conexion.png)

---

### 2. Transferencia Bidireccional de Archivos 🔄

He verificado el funcionamiento del servidor realizando operaciones en ambos sentidos:

1.  **Subida (Upload):** He arrastrado un archivo desde mi equipo local hacia el panel derecho (servidor).
2.  **Descarga (Download):** He recuperado un archivo del servidor hacia mi carpeta local.
3.  **Observación de Estados:** He monitorizado la consola superior, donde se confirman comandos como `TYPE I` (binario), `PASV` (modo pasivo) y `STOR`/`RETR` para la transferencia.

![captura-transferencia-correcta](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20con%20clientes%20gr%C3%A1ficos/transferencia-exito.png)

---

### 3. Conclusión de las Pruebas Gráficas

El uso de un cliente GUI permite una gestión mucho más visual y segura. Gracias a la configuración del **Modo Pasivo** realizada en la Actividad 5 y los **Permisos de Escritura** ajustados, la transferencia de archivos de gran tamaño se realiza sin interrupciones y con feedback visual constante sobre el progreso.

![captura-mensajes-estado](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20con%20clientes%20gr%C3%A1ficos/log-final.png)
