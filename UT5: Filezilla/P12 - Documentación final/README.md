# 📂 PROYECTO FINAL: DESPLIEGUE DE SERVIDOR FTP SEGURO
## U.T. 5 - Gestión de Servicios de Transferencia de Archivos

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Documentaci%C3%B3n%20final/logo.jpg)

**Estudiante:** Basi Córdoba Arcas  
**Curso:** 2º DAW  
**Fecha de entrega:** 20/02/2026  
**Tecnologías:** FileZilla Server, FileZilla Client, TLS/SSL, Apache.

---

## 📑 Índice de Contenidos
1. [Introducción e Instalación](#1-introducción-e-instalación)
2. [Configuración de Red: Modos Activo y Pasivo](#2-configuración-de-red-modos-activo-y-pasivo)
3. [Gestión de Usuarios y Permisos](#3-gestión-de-usuarios-y-permisos)
4. [Seguridad y Cifrado (FTPS)](#4-seguridad-y-cifrado-ftps)
5. [Análisis de Clientes (CLI, GUI, Browser)](#5-análisis-de-clientes-cli-gui-browser)
6. [Integración con Servidor Web](#6-integración-con-servidor-web)
7. [Buenas Prácticas de Administración](#7-buenas-prácticas-de-administración)

---

### 1. Introducción e Instalación 🛠️
Se ha procedido a la instalación de **FileZilla Server v1.9.4** en un entorno Windows. Durante el proceso, se ha configurado el servicio para iniciarse automáticamente con el sistema, estableciendo una contraseña de administración robusta y definiendo los puertos de escucha estándar (21 para FTP).

### 2. Configuración de Red: Modos Activo y Pasivo 🌐
Uno de los retos técnicos fue la configuración del **Modo Pasivo**.
* **Firewall:** Se habilitaron reglas para los puertos de control y el rango de puertos dinámicos.
* **Rango Pasivo:** Se definió el rango $50000-50100$ para evitar conflictos de conexión detrás de routers o firewalls.

### 3. Gestión de Usuarios y Permisos 👥
Se implementó una estructura jerárquica mediante **Grupos**:
* **Grupo Anónimo:** Acceso limitado a solo lectura.
* **Grupo Clientes_Limitados:** Acceso mediante credenciales con permisos de escritura.
* **Control de Errores:** Se identificaron y corrigieron errores de tipo `550 Permission denied` ajustando las políticas de escritura del servidor.

### 4. Seguridad y Cifrado (FTPS) 🔒
Para proteger las credenciales y los datos:
* **Certificado:** Se generó un certificado X.509 auto-firmado con cifrado Ed25519.
* **Cifrado Explícito:** Se configuró el servidor para obligar el uso de **TLS 1.2+**, denegando conexiones inseguras.
* **Verificación:** La conexión del `usuario_1` confirma el establecimiento de un túnel seguro.

### 5. Análisis de Clientes (CLI, GUI, Browser) 💻
Se compararon tres métodos de acceso:
1. **CLI (Línea de comandos):** Rápido pero limitado a transferencias básicas sin TLS por defecto.
2. **GUI (FileZilla Client):** Método recomendado por su soporte completo de FTPS y feedback visual.
3. **Navegador:** Se constató la obsolescencia del protocolo `ftp://` en navegadores modernos como Chrome.

### 6. Integración con Servidor Web 🚀
Se vinculó el servidor FTP con un entorno **Apache (XAMPP)** mediante un *Mount Point* en la carpeta `htdocs`. Esto permite un flujo de publicación donde los archivos subidos por FTP son servidos instantáneamente vía HTTP.

### 7. Buenas Prácticas de Administración 🛡️
Como recomendaciones finales para un entorno de producción, se destaca la importancia de:
* Mantener el **Cifrado TLS** obligatorio.
* Monitorizar los **Logs** para auditoría.
* Realizar copias de seguridad de la configuración XML y los certificados.

---

## 🏁 Conclusión
Este proyecto demuestra que la implementación de un servidor FTP no se limita a compartir archivos, sino que requiere una gestión precisa de la seguridad, la red y los permisos para garantizar la integridad de la información en un entorno DAW.
