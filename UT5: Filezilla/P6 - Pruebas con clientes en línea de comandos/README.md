> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20con%20clientes%20en%20l%C3%ADnea%20de%20comandos/logo.jpg)

> ### U.T. 5 **Actividad 6: Pruebas con clientes en línea de comandos ⌨️🚀**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Introducción al uso de CLI en FTP

Aunque los clientes con interfaz gráfica como FileZilla son cómodos, en entornos de servidores reales (como Linux sin escritorio) es necesario dominar la línea de comandos. He utilizado el cliente estándar **`ftp`** de Windows para realizar las pruebas de conexión y gestión de archivos.

---

### 2. Conexión y Autenticación

Para iniciar la sesión, he abierto el **Símbolo del sistema (CMD)** y he ejecutado los siguientes pasos:

1.  **Comando de inicio:** `ftp 127.0.0.1`
2.  **Usuario:** `usuario_1` (o el creado en la Actividad 3).
3.  **Contraseña:** `********`

![captura-conexion-cli](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20con%20clientes%20en%20l%C3%ADnea%20de%20comandos/usuario1-cmd.png)

---

### 3. Operaciones Realizadas

He ejecutado las tres operaciones básicas solicitadas para verificar el control total sobre el servidor:

| Operación | Comando Utilizado | Función |
| :--- | :--- | :--- |
| **Listar** | `ls` o `dir` | Muestra los archivos y carpetas en el directorio actual del servidor. |
| **Descargar** | `get archivo.txt` | Transfiere un archivo desde el servidor a mi carpeta local actual. |
| **Subir** | `put local.txt` | Sube un archivo desde mi PC hacia el directorio raíz del servidor FTP. |
| **Salir** | `bye` o `quit` | Cierra la sesión y finaliza la conexión con el servidor. |

![captura-operaciones-cli](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Pruebas%20con%20clientes%20en%20l%C3%ADnea%20de%20comandos/pruebatxt-usuario.png)

---

### 4. Documentación de Comandos y su Función

* **`open [IP] [Puerto]`**: Abre una conexión si no se hizo al arrancar el cliente.
* **`user [nombre]`**: Permite identificarse con una cuenta específica.
* **`binary`**: Cambia el modo de transferencia a binario (recomendado para imágenes o ejecutables).
* **`ascii`**: Cambia el modo de transferencia a texto (para archivos .txt o .html).
* **`hash`**: Muestra una marca visual (#) por cada bloque de datos transferido (útil para ver el progreso).
