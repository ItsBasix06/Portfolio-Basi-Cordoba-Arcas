> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Herramientas%20de%20administraci%C3%B3n%20%E2%80%94%20Manager%20y%20Host%20Manager/logo.jpg)

> ### U.T. 4 **Practica 6: Herramientas de administración — Manager y Host Manager**

**Curso:** 2ºDAW
**Autor:** Basi Córdoba Arcas
**Fecha:** 04/02/2026

---

> ### 1. Acceso a las Interfaces 🚪

Tomcat proporciona dos potentes herramientas web integradas para la gestión del servidor. Para poder acceder a ellas, es necesario contar con un usuario configurado previamente en el archivo `tomcat-users.xml` que posea los roles específicos requeridos:
* Para el Manager: Rol `manager-gui`
* Para el Host Manager: Rol `admin-gui`

Una vez configurados los permisos y levantado el servicio, accedo a través del navegador web a las siguientes rutas:

![captura-pantalla-login](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Herramientas%20de%20administraci%C3%B3n%20%E2%80%94%20Manager%20y%20Host%20Manager/login-admin.png)

---

> ### 2. Ficha Descriptiva: Tomcat Web Application Manager 🛠️

Esta herramienta permite administrar de forma visual las aplicaciones web (contextos) que están instaladas en el servidor, sin necesidad de reiniciar Tomcat ni usar la línea de comandos.

| Característica | Detalle |
| :--- | :--- |
| **URL de Acceso** | `http://localhost:8080/manager/html` (o puerto seguro 8443) |
| **Rol necesario** | `manager-gui` |
| **Función: Despliegue (Deploy)** | Permite instalar nuevas aplicaciones web. Se puede hacer subiendo directamente un archivo empaquetado `.war` desde nuestro equipo local, o especificando la ruta física del directorio en el servidor. |
| **Función: Recarga (Reload)** | Reinicia una aplicación web específica sin afectar a las demás ni al servidor completo. Muy útil tras hacer pequeños cambios en el código (clases Java o descriptores `web.xml`) para que los cambios surtan efecto. |
| **Función: Parada / Arranque** | Los botones *Stop* y *Start* permiten detener temporalmente una aplicación (mostrando un error HTTP a quien intente entrar) o volver a habilitarla. |
| **Función: Re-despliegue (Undeploy)** | Elimina por completo la aplicación web del servidor, borrando su carpeta dentro del directorio `webapps`. |
| **Estado del Servidor** | En la parte superior ofrece acceso a `Server Status`, donde se puede monitorizar el uso de memoria (JVM), la carga del servidor y el estado de los puertos. |

![captura-panel-manager](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Herramientas%20de%20administraci%C3%B3n%20%E2%80%94%20Manager%20y%20Host%20Manager/login.png)

---

> ### 3. Ficha Descriptiva: Tomcat Virtual Host Manager 🌐

Esta interfaz está diseñada para gestionar la infraestructura de dominios. Un Host Virtual permite que una única instancia de Tomcat atienda peticiones para múltiples nombres de dominio diferentes (por ejemplo, `misitio1.com` y `misitio2.com`), dirigiendo a cada uno a su propia carpeta de aplicaciones.

| Característica | Detalle |
| :--- | :--- |
| **URL de Acceso** | `http://localhost:8080/host-manager/html` |
| **Rol necesario** | `admin-gui` |
| **Creación de Hosts Virtuales** | Permite registrar nuevos dominios (Host). Al crearlo, se le asigna un nombre y un directorio `appBase` específico dentro del servidor (distinto al `webapps` por defecto) donde se guardarán exclusivamente las aplicaciones de ese dominio. |
| **Gestión de Alias** | Se pueden añadir alias a un host existente. Por ejemplo, si el host es `midominio.local`, podemos añadir el alias `www.midominio.local` para que ambos respondan al mismo contenido. |
| **Control del Ciclo de Vida** | Al igual que con las aplicaciones, podemos Iniciar (Start), Detener (Stop) o Eliminar (Remove) hosts enteros. Detener un host desconecta inmediatamente todos los dominios y aplicaciones asociados a él. |

![captura-panel-host-manager](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Herramientas%20de%20administraci%C3%B3n%20%E2%80%94%20Manager%20y%20Host%20Manager/host-manager.png)
