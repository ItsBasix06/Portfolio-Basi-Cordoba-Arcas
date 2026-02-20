> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Uso%20del%20navegador%20como%20cliente%20FTP/logo.jpg)

> ### U.T. 5 **Actividad 9: Uso del navegador como cliente FTP 🌐📂**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Intento de Acceso desde el Navegador

He intentado acceder al servidor mediante la URL `ftp://127.0.0.1` desde el navegador Google Chrome. 

* **Resultado:** El navegador no muestra el contenido. En su lugar, lanza un aviso indicando que necesita abrir una aplicación externa para gestionar el protocolo.
* **Evidencia:** Como se observa en la captura, Chrome intenta derivar la conexión a Microsoft Edge o al sistema operativo al carecer de soporte nativo.

![captura-error-navegador](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Uso%20del%20navegador%20como%20cliente%20FTP/captura-error-navegador.png)

---

### 2. Comparativa: Navegador vs. Cliente Dedicado

A continuación, se detallan las limitaciones observadas al comparar el uso de un navegador frente a herramientas como **FileZilla Client**.

| Característica | Navegador Web (Chrome/Edge/Firefox) | Cliente Dedicado (FileZilla/WinSCP) |
| :--- | :--- | :--- |
| **Soporte de Protocolos** | Muy limitado o inexistente (obsoleto). | Soporta FTP, FTPS, SFTP, etc. |
| **Seguridad (TLS)** | Pobre gestión de certificados. | Soporte total para certificados y cifrado. |
| **Operaciones** | Generalmente solo permite lectura/descarga. | Permite subir, bajar, renombrar y editar. |
| **Gestión de Archivos** | Un archivo a la vez. | Transferencias múltiples y colas de espera. |
| **Velocidad** | Lenta, no optimizada para datos. | Muy alta, optimizada para grandes volúmenes. |

---

### 3. Ventajas y Desventajas (Resumen)

**Ventajas:**
* **Universalidad:** No requiere instalar software adicional (si el navegador aún lo soporta).
* **Simplicidad:** Interfaz conocida por cualquier usuario básico.
* **Ideal para descargas rápidas:** Útil para servidores públicos de drivers o manuales.

**Desventajas:**
* **Inseguro:** No suele manejar bien el FTPS configurado en la Actividad 8.
* **Unidireccional:** Normalmente no permite subir archivos (`PUT`).
* **Sin control técnico:** No muestra los logs de comandos `STOR`, `RETR` o `PASV`.

---

### 4. Conclusión Final

Aunque el navegador puede servir como un cliente de "emergencia" para visualizar archivos públicos, para la administración profesional de un servidor FTP es imprescindible contar con un cliente dedicado. La seguridad implementada en nuestro servidor (TLS Obligatorio) hace que la mayoría de navegadores actuales no puedan ni siquiera establecer la conexión inicial.
