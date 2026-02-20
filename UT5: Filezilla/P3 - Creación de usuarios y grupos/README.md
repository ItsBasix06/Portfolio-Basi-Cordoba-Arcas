> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Creaci%C3%B3n%20de%20usuarios%20y%20grupos/logo.jpg)

> ### U.T. 5 **Actividad 3: Creación de usuarios y grupos 👥🔐**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Creación de un Grupo con Permisos Limitados

En la gestión de servidores, el uso de grupos permite aplicar políticas de seguridad de forma masiva. He creado un grupo llamado **`Clientes_Limitados`**. 

A este grupo se le ha asignado:
* **Mount Point (Punto de montaje):** He mapeado una carpeta física de mi disco duro (ej. `C:\ftp_datos`) a la ruta virtual raíz (`/`) del servidor FTP.
* **Permisos:** Se han limitado los permisos solo a **Lectura (Read)** y **Listado (List)**, denegando la Escritura (Write) y el Borrado (Delete) para asegurar que los usuarios no modifiquen el contenido.

![captura-configuracion-grupo](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Creaci%C3%B3n%20de%20usuarios%20y%20grupos/captura-configuracion-grupo.png)

---

### 2. Creación de Usuarios Asociados

Siguiendo los requisitos, he creado dos usuarios distintos que heredan la configuración del grupo anterior:
1.  **`usuario_1`**
2.  **`usuario_2`**

Ambos usuarios están integrados en el grupo `Clientes_Limitados`, por lo que comparten el mismo directorio raíz y las mismas restricciones de seguridad sin necesidad de configurarlos uno por uno.

![captura-usuarios-creados](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Creaci%C3%B3n%20de%20usuarios%20y%20grupos/captura-usuarios-creados.png)

---

### 3. Definición de Límites de Conexión ⏳

Para evitar la saturación del servidor por un solo usuario, se han establecido límites de conexión en la sección **Access Control** o **Connection Limits**:
* **Maximum concurrent connections:** Limitado a **2** conexiones por usuario.
* **IP Limit:** Se permite la conexión desde cualquier IP, pero con un máximo de hilos simultáneos.

![captura-limites-conexion](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Creaci%C3%B3n%20de%20usuarios%20y%20grupos/captura-limites-conexion.png)

---

### 4. Diferencias: Permisos de Usuario vs. Permisos de Grupo 🆚

| Característica | Permisos de Grupo | Permisos de Usuario |
| :--- | :--- | :--- |
| **Aplicación** | Se aplican a todos los miembros que pertenecen al grupo. | Se aplican de forma individual y específica a una cuenta. |
| **Escalabilidad** | Alta. Si cambias un permiso en el grupo, se actualiza para 100 usuarios a la vez. | Baja. Habría que cambiar la configuración usuario por usuario. |
| **Prioridad** | Actúan como base general. | Tienen prioridad (override). Pueden dar un permiso extra a un usuario concreto que el grupo no tiene. |
| **Uso ideal** | Para definir políticas generales de la empresa o departamento. | Para casos excepcionales o administradores con privilegios únicos. |

---

### 5. Verificación de Directorios y Permisos (Mount Points) 📂

He configurado el directorio raíz para que los usuarios, al loguearse, aterricen directamente en la carpeta de intercambio de archivos profesional.

![captura-mount-points](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Creaci%C3%B3n%20de%20usuarios%20y%20grupos/captura-mount-points.png)
