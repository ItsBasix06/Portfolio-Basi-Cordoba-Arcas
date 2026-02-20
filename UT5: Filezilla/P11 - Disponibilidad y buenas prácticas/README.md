> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Disponibilidad%20y%20buenas%20pr%C3%A1cticas/logo.jpg)

> ### U.T. 5 **Actividad 11: Disponibilidad y buenas prácticas 🛡️💎**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Recomendaciones para un Entorno de Producción

Para garantizar que el servidor FTP sea robusto y profesional, se han definido las siguientes directrices basadas en la configuración realizada durante las prácticas anteriores.

#### A. Límites de Conexión y Rendimiento ⚖️
* **Restricción de IPs:** Limitar el número de conexiones por IP para evitar ataques de Denegación de Servicio (DoS).
* **Timeout:** Configurar un tiempo de espera de desconexión automática (ej. 120 segundos) para liberar puertos ocupados por sesiones inactivas.
* **Ancho de Banda:** Aplicar límites de velocidad de subida y bajada por usuario o grupo para no saturar la red del servidor.

#### B. Logs y Auditoría de Seguridad 🔍
* **Registro de Actividad:** Es vital monitorizar los mensajes de estado para detectar intentos de acceso fallidos o movimientos sospechosos.
* **Rotación de Logs:** Configurar FileZilla para que guarde los registros en archivos diarios y los borre cada 30 días para no agotar el espacio en disco.
* **Análisis de Errores:** Supervisar errores como el "550 Permission Denied" para detectar configuraciones de permisos incorrectas en tiempo real.

#### C. Copias de Seguridad (Backups) 💾
* **Configuración del Servidor:** Exportar regularmente el archivo XML de configuración de FileZilla Server (usuarios, grupos y certificados).
* **Datos de Usuario:** Realizar backups incrementales de las carpetas físicas (como `htdocs`) vinculadas al servidor.
* **Certificados TLS:** Guardar en un lugar seguro y fuera del servidor los archivos `.crt` y `.key` generados.

#### D. Red: Firewall y NAT 🌐
* **Modo Pasivo:** Mantener siempre el rango de puertos (50000-50100) abierto en el firewall para asegurar la compatibilidad con clientes externos.
* **Cifrado Obligatorio:** No permitir nunca conexiones en texto plano (`plain FTP`) en producción; forzar siempre el uso de TLS explícito.

---

### 2. Evidencias de Implementación

Durante el despliegue se han aplicado estas buenas prácticas:

1.  **Seguridad en Capa de Red:** Se han habilitado las reglas específicas en el Firewall de Windows para FileZilla Server y Client.
2.  **Cifrado de Datos:** Se ha generado un certificado TLS con validez de un año para asegurar el canal.
3.  **Gestión de Sesiones:** La verificación final con el `usuario_1` demuestra un túnel seguro establecido y una transferencia monitorizada.

![captura-final-produccion](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Disponibilidad%20y%20buenas%20pr%C3%A1cticas/firewall.png)

---

### 3. Conclusión Final del Proyecto

El despliegue del servidor FileZilla ha cumplido con todos los requisitos técnicos y de seguridad exigidos. La integración con servicios web y el uso de estándares de cifrado actuales garantizan un servicio de transferencia de archivos profesional, escalable y seguro.
