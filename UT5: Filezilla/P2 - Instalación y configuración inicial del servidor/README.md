> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20inicial%20del%20servidor/logo.jpg)

> ### U.T. 5 **Actividad 2: Instalación y configuración inicial de FileZilla Server 🛠️⚙️**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Instalación del Servidor

Para esta práctica, instalamos **FileZilla Server**. Durante el proceso de instalación, es fundamental prestar atención a dos aspectos clave:
1.  **Puerto de la Interfaz de Administración:** Por defecto es el `14148`. Es el puerto que usa la "consola" para hablar con el "motor" del servidor.
2.  **Contraseña de Administración:** Se define una contraseña fuerte para proteger el acceso a la configuración del servidor.

![captura-proceso-instalacion](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20inicial%20del%20servidor/captura-proceso-instalacion.png)

---

### 2. Acceso a la Consola de Administración

Una vez instalado, abrimos la aplicación **FileZilla Server Administration Interface**. 
* Al iniciar, nos pide conectarnos al "servidor local" (`127.0.0.1`) usando el puerto de administración definido anteriormente.
* Introducimos la contraseña establecida durante la instalación.

![captura-consola-administracion](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20inicial%20del%20servidor/captura-consola-administracion.png)

---

### 3. Configuración Inicial (Listen Port e IP) 🌐

Para que el servidor sea funcional, debemos configurar por dónde va a recibir a los clientes. Entramos en **Settings > FTP Server > Listeners**:

* **Puerto de escucha (FTP):** Configuramos el puerto estándar **21**. Si quisiéramos usar un puerto no estándar por seguridad (ofuscación), podríamos cambiarlo aquí.
* **Dirección IP:** En el apartado de *IP Bindings*, seleccionamos `*` o `0.0.0.0`. Esto indica al servidor que debe escuchar peticiones a través de **todas las interfaces de red** disponibles en la máquina (Ethernet, Wi-Fi, Loopback).

![captura-configuracion-puerto-ip](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20inicial%20del%20servidor/captura-configuracion-puerto-ip.png)

---

### 4. Configuración del Inicio Automático 🔄

Es vital que el servidor FTP se inicie solo cada vez que arranquemos la máquina, sin necesidad de abrir la interfaz manualmente.

* **En Windows:** El instalador configura FileZilla Server como un **Servicio de Windows**. Verificamos en `services.msc` que el tipo de inicio esté en **Automático**.

De esta forma, garantizamos la disponibilidad del servicio de transferencia de archivos tras cualquier reinicio del sistema.

![captura-servicio-automatico](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20inicial%20del%20servidor/captura-servicio-automatico.png)

---

### 5. Verificación del Servicio 🕵️✅

Tras aplicar los cambios (clic en "OK" y confirmar en el log), comprobamos que en la parte inferior de la consola de administración aparece el mensaje:
> `Server online` o `Logged on to server`

Esto indica que el motor del servidor está corriendo, el puerto 21 está abierto y el sistema está listo para crear usuarios y compartir carpetas.

![captura-final-servicio-funcionando](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20inicial%20del%20servidor/captura-final-servicio-funcionando.png)

---

### Resumen de la Configuración Realizada

| Parámetro | Valor Configurado | Descripción |
| :--- | :--- | :--- |
| **Admin Port** | 14148 | Puerto para la gestión interna del servidor. |
| **FTP Port** | 21 | Puerto estándar para conexiones de clientes. |
| **IP Binding** | 0.0.0.0 (*) | Escucha en todas las tarjetas de red. |
| **Startup Type** | Automático | El servicio arranca con el Sistema Operativo. |
