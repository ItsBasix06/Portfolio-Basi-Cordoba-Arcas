> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web
> ### U.T. 5 **Actividad 1: Introducción y arquitectura de FileZilla Server 📂🚀**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Introducción

En esta nueva unidad de trabajo nos centraremos en el despliegue de servidores para la transferencia de archivos. Antes de proceder con la instalación y configuración práctica de **FileZilla Server**, es imprescindible comprender los fundamentos teóricos del protocolo FTP. Su arquitectura particular, basada en el uso de múltiples canales y puertos, lo diferencia de otros servicios web (como HTTP) y suele ser una fuente común de problemas de configuración de red y firewalls.

---

### 2. Conceptos Básicos: Protocolos de Transferencia

Aunque coloquialmente hablamos de "servidor FTP", existen diferentes protocolos para mover archivos, cada uno con sus características de seguridad y funcionamiento:

| Protocolo | Nombre Completo | Descripción y Seguridad | Puerto Habitual |
| :--- | :--- | :--- | :--- |
| **FTP** | File Transfer Protocol | El protocolo original estándar. **Inseguro**: transmite el usuario, la contraseña y los datos en texto plano, por lo que cualquiera que capture el tráfico puede leerlos. | TCP 21 |
| **FTPS** | FTP over SSL/TLS | Es el protocolo FTP estándar pero envuelto en una capa de cifrado SSL/TLS (similar a cómo HTTPS es HTTP seguro). **Seguro**. Es el que utilizaremos principalmente con FileZilla Server. | TCP 21 (Explícito) / 990 (Implícito) |
| **SFTP** | SSH File Transfer Protocol | No tiene relación técnica con FTP. Es un subsistema del protocolo SSH (Secure Shell), el mismo usado para administrar servidores Linux remotamente. **Muy seguro**, utiliza un solo puerto para todo. | TCP 22 |

---

### 3. Arquitectura Cliente-Servidor y Puertos Implicados

El protocolo FTP utiliza una arquitectura cliente-servidor peculiar. A diferencia de HTTP, que usa una sola conexión para pedir una página y recibirla, FTP utiliza **dos canales separados** para operar:

1.  **Canal de Control (Puerto 21):**
    * Es la "línea de comandos".
    * El cliente se conecta al puerto 21 del servidor.
    * Por aquí se envían órdenes como "iniciar sesión", "cambiar de directorio", "borrar archivo" o "prepárate para recibir datos".
    * Esta conexión permanece abierta durante toda la sesión.

2.  **Canal de Datos (Puertos dinámicos/aleatorios):**
    * Es la "tubería" por donde viajan los archivos reales y los listados de directorios.
    * Se abre una conexión de datos *nueva* cada vez que se transfiere un archivo o se lista una carpeta, y se cierra al terminar.
    * El gran dilema de FTP es: **¿Quién abre esta segunda conexión y en qué puerto?** La respuesta depende del modo de conexión (Activo o Pasivo).

---

### 4. Tarea: Esquema del Flujo de Conexión (Activo vs Pasivo)

El siguiente esquema ilustra las diferencias críticas entre los dos modos de funcionamiento de FTP, mostrando cómo se establecen el canal de control y el de datos, y por qué el modo pasivo es el estándar hoy en día para atravesar firewalls.

![Esquema del flujo de conexión FTP: Activo vs. Pasivo](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Introducci%C3%B3n%20y%20arquitectura%20de%20FileZilla%20Server/logo.jpg)

#### Análisis del Esquema:

* **MODO ACTIVO (Active Mode - Izquierda):**
    * **Flujo:** El cliente se conecta al puerto 21 (Control). Cuando quiere datos, el cliente abre un puerto aleatorio local (ej. puerto N) y le dice al servidor "Conéctate a mi puerto N para enviarme los datos". El servidor inicia la conexión desde su puerto 20 hacia el puerto N del cliente.
    * **Problema:** El firewall del cliente suele bloquear las conexiones entrantes no solicitadas. Por eso este modo falla en la mayoría de redes modernas (hogares, oficinas con NAT).

* **MODO PASIVO (Passive Mode - Derecha):**
    * **Flujo:** El cliente se conecta al puerto 21 (Control) y envía el comando `PASV`. El servidor responde abriendo un puerto aleatorio en su lado (ej. puerto P) e informando al cliente: "OK, conéctate a mi IP en el puerto P para los datos". El cliente inicia la conexión de datos hacia el servidor.
    * **Ventaja:** Como es el cliente quien inicia ambas conexiones (Control y Datos) hacia afuera, los firewalls del lado del cliente suelen permitirlo sin problemas.
    * **Requisito en el Servidor:** FileZilla Server debe configurarse para definir un "Rango de puertos pasivos" y permitir ese rango en el firewall del servidor.
