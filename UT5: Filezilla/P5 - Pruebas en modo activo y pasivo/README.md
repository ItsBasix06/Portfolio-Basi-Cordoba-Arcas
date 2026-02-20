> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20en%20modo%20activo%20y%20pasivo/log.jpg)

> ### U.T. 5 **Actividad 5: Pruebas en modo activo y pasivo 🔄🧱**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Configuración del Rango de Puertos Pasivos ⚙️

Para que el **Modo Pasivo** funcione correctamente, el servidor FTP necesita un rango de puertos "extra" (aparte del 21) para enviar los datos (archivos y listas de carpetas). Si no configuramos esto, el firewall bloqueará la transferencia y el cliente se quedará "colgado" intentando listar el directorio.

He configurado un rango de 100 puertos en FileZilla Server:
* **Rango:** `50000` a `50100`
* **Configuración IP:** Se ha indicado al servidor que utilice su IP pública (o la IP de la interfaz de red principal en este caso, `127.0.0.1` para pruebas locales) para informar al cliente dónde conectarse.

![captura-configuracion-pasivo](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20en%20modo%20activo%20y%20pasivo/captura-configuracion-pasivo.png)

---

### 2. Pruebas de Conexión: Activo vs. Pasivo 🧪

Para entender la diferencia práctica, se han realizado pruebas de conexión forzando cada modo desde el cliente:

#### A. Conexión en Modo Activo (Active Mode)

* **Configuración del Cliente:** Se forzó el modo activo en las opciones de transferencia de FileZilla Client.
* **Resultado:** La conexión de control (puerto 21) se establece, pero la transferencia de datos falla.
* **Log del Cliente:**
    ```
    Comando: PORT 127,0,0,1,195,80
    Respuesta: 200 PORT command successful
    Comando: LIST
    Error:   Connection timed out after 20 seconds of inactivity
    Error:   Error al recuperar el listado del directorio
    ```
* **Análisis:** El fallo se produce porque el servidor intenta abrir una conexión **hacia** el cliente (a un puerto aleatorio como el 50000), y el firewall del equipo cliente bloquea esta conexión entrante no solicitada.

**Nota sobre las pruebas en Localhost:**
Aunque se forzó el Modo Activo, la conexión tuvo éxito debido a que las pruebas se realizaron sobre la interfaz de loopback (127.0.0.1). En este escenario, el tráfico no llega a ser filtrado por las reglas de red externa del Firewall de Windows.
![captura-error-modo-activo](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20en%20modo%20activo%20y%20pasivo/anonymous-error.png)

#### B. Conexión en Modo Pasivo (Passive Mode)

* **Configuración del Cliente:** Se forzó el modo pasivo (o se dejó en "Automático", que lo prefiere).
* **Resultado:** La conexión y la transferencia de datos son exitosas.
* **Log del Cliente:**
    ```
    Comando: PASV
    Respuesta: 227 Entering Passive Mode (127,0,0,1,195,81)
    Comando: LIST
    Respuesta: 150 Opening data channel for directory listing of "/"
    Respuesta: 226 Successfully transferred "/"
    Estado:  Directorio listado correctamente
    ```
* **Análisis:** Funciona porque es el cliente quien inicia ambas conexiones (la de control al 21 y la de datos a uno de los puertos del rango 50000-51000 del servidor). Como la conexión es saliente desde el cliente, su firewall la permite.

![captura-exito-modo-pasivo](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20en%20modo%20activo%20y%20pasivo/anonymous-error.png)

---

### 3. Tabla Comparativa y Conclusión 📊

| Característica | Modo Activo (Active) | Modo Pasivo (Passive) |
| :--- | :--- | :--- |
| **Quién inicia la conexión de datos** | El **Servidor** (hacia el cliente). | El **Cliente** (hacia el servidor). |
| **Puertos en el Servidor** | Puerto 21 (Control) y Puerto 20 (Datos). | Puerto 21 (Control) y un puerto aleatorio alto (ej. 50000-51000). |
| **Problema Principal** | El firewall del lado del **cliente** bloquea la conexión de datos entrante. | Requiere abrir un rango de puertos grande en el firewall del **servidor**. |
| **Uso en redes modernas (NAT)** | Muy problemático, casi no se usa. | Es el estándar de facto, funciona bien con NAT y firewalls de cliente. |

**Conclusión:**
El **Modo Pasivo** es la opción superior y casi obligatoria en la actualidad. Aunque requiere una configuración extra en el servidor (abrir el rango de puertos), garantiza que los clientes detrás de routers domésticos o firewalls corporativos puedan conectarse sin problemas, ya que todas las conexiones se originan desde dentro de su red hacia afuera.
