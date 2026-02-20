> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Configuraci%C3%B3n%20de%20acceso%20an%C3%B3nimo/logo.jpg)

> ### U.T. 5 **Actividad 4: Configuración de acceso anónimo 👤🌐**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Definición del Acceso Anónimo

El acceso anónimo permite que los usuarios se conecten al servidor FTP utilizando el nombre de usuario `anonymous` o `ftp`. En esta configuración, no se requiere una contraseña (o se acepta cualquier correo electrónico como tal), facilitando la distribución pública de archivos.

Para cumplir con los requisitos de seguridad, se ha configurado este acceso bajo el principio de **mínimo privilegio**.

---

### 2. Configuración del Usuario Anónimo

En FileZilla Server, he creado un usuario específico con las siguientes características:
* **Username:** `anonymous`
* **Password:** Desactivada (No password required).
* **Grupo:** Ninguno (para tener un control total e independiente sobre este usuario público).

![captura-usuario-anonimo](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Configuraci%C3%B3n%20de%20acceso%20an%C3%B3nimo/anonymous-creacion.png)

---

### 3. Restricción de Directorio y Permisos 📂🚫

Para evitar que un usuario anónimo pueda navegar por todo el servidor o subir archivos maliciosos, se ha limitado su alcance:

1.  **Directorio limitado:** Se ha creado una carpeta física específica llamada `C:\ftp_publico`.
2.  **Mount Point:** Se ha mapeado como directorio raíz (`/`) para este usuario.
3.  **Permisos de Solo Lectura:**
    * **Read:** Activado.
    * **List:** Activado.
    * **Write/Delete/Create:** Desactivados.

![captura-permisos-anonimo](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Configuraci%C3%B3n%20de%20acceso%20an%C3%B3nimo/captura-permisos-anonimo.png)

---

### 4. Prueba de Conexión desde Cliente FTP 🧪

He realizado la comprobación utilizando **FileZilla Client** desde una máquina cliente (o la misma IP local):

* **Host:** `127.0.0.1` (o la IP del servidor)
* **Username:** `anonymous`
* **Password:** (en blanco)
* **Resultado:** Conexión exitosa. El servidor permite listar y descargar archivos de la carpeta pública, pero deniega cualquier intento de subida o borrado.

![captura-prueba-conexion-exitosa](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Configuraci%C3%B3n%20de%20acceso%20an%C3%B3nimo/anonymous-file-cliente.png)

---

### 5. Documentación de Resultados

Al conectar como `anonymous`, el log del servidor muestra una entrada exitosa sin validación de contraseña. Si intento arrastrar un archivo desde mi PC al servidor, el cliente devuelve el error: `550 Permission denied`, lo que confirma que las políticas de seguridad de la Actividad 4 se están aplicando correctamente.
