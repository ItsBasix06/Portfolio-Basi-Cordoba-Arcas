> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web



![img](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Identificaci%C3%B3n%20de%20archivos%20de%20configuraci%C3%B3n/logo.jpg)



> ### U.T. 4 **Practica 2: Identificación de archivos de configuración de Tomcat🐱⚙️**

**Curso:** 2ºDAW


**Autor:** Basi Córdoba Arcas

**Fecha:** 23/01/2025



> ### 📥🐱 Instalación de Tomcat

Antes de empezar con la localizacion de los archivos clave de Tomcat, me he asegurado si tengo Tomcat instalado en el sistema con `dpkg -l | grep tomcat` y por lo que veo no hubo muy buena señal directamente ni me aparecia, por ello vamos a proceder con la descarga e instalacion de tomcat.


- **Pasos a seguir**
  1. Hacer un `sudo apt update`.
  2. Hacer un `sudo apt upgrade`.
  3. Intalar `Tomcat` y sus `herramientras de administracion`

  
Una vez llegado al paso 3, el comando para poder instalar tomcat y sus herramientras de administracion es el siguiente:
```bash
sudo apt install tomcat10 tomcat10-admin -y
```
![instalacion-tomcat](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Identificaci%C3%B3n%20de%20archivos%20de%20configuraci%C3%B3n/instalacion-tomcat.png)

> **🔍🐱📁 Localizar archivos clave de Tomcat**

Los archivos se localizan en mi caso en `/etc/Tomcat` y ahi se puede ver los archivos, segun la practica proporcionada por el profesor, la ruta correcta para encontrar los .xml es dentro de `/conf/tomccat`, sin embargo yo lo he instalado por `apt` y por eso cambia ya que organiza las carpetas y en la practica desde la `pagina oficial`,esa es la diferencia de porque me sale en otro lado,aqui tienes un vistazo de la carpeta `Tomcat`:


![vistazo-carpeta-tomcat](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Identificaci%C3%B3n%20de%20archivos%20de%20configuraci%C3%B3n/vistazo-carpeta-tomcat.png)



> ### etc/server.xml ⚙️📜


Es el `archivo de configuración principal de Tomcat`. Si Tomcat fuera un edificio, el `server.xml` serían los `planos de la estructura:` define qué puertas están abiertas (puertos), cuántas alas tiene el edificio (servicios) y quién vive en cada planta (hosts).

- **Función Principal⚙️✅**

Su función es `definir la arquitectura de componentes del servidor.` Determina cómo recibe Tomcat las peticiones de red y cómo las procesa internamente.

| Elemento | Qué configura | Ejemplo de uso |
| :--- | :--- | :--- |
| **`<Server>`** | Es el elemento raíz que representa a todo el servidor Tomcat. | Configurar el puerto de "apagado" (shutdown) para detener el proceso de forma segura. |
| **`<Service>`** | Agrupa uno o más **Connectors** que comparten un mismo motor de procesamiento (**Engine**). | Permite separar lógicamente diferentes servicios dentro de una misma instancia de Tomcat. |
| **`<Connector>`** | Define los puntos de entrada de red (puertos) y los protocolos de comunicación. | Cambiar el puerto por defecto de **8080** a **80** o configurar certificados **SSL/TLS (HTTPS)**. |
| **`<Engine>`** | Es el motor encargado de procesar todas las peticiones que llegan a través de los conectores. | Define el motor de renderizado y procesamiento predeterminado para un servicio específico. |
| **`<Host>`** | Define los **Hosts Virtuales**, que permiten asociar nombres de dominio a aplicaciones. | Configurar Tomcat para que gestione varios dominios (ej: `app1.com` y `app2.com`) de forma independiente. |

> ### etc/web.xml 🌐⚙️

Es el `manual de convivencia` de todas tus aplicaciones. Es el archivo donde le dices a Tomcat: **"Oye, por defecto, quiero que todas las webs que yo suba aquí se comporten de esta manera"**.

- **Función Principal⚙️✅**

Establece los valores predeterminados. Si una aplicación no dice lo contrario, usará los tiempos de sesión, los tipos de archivos y las páginas de error que tú escribas aquí.

| Elemento | Qué configura |
| :--- | :--- |
| **`<session-config>`** | Establece cuánto tiempo tarda la sesión del usuario en caducar por inactividad (por defecto **30 min**). |
| **`<welcome-file-list>`** | Define la lista de archivos que se abren por defecto al entrar a una carpeta (ej. `index.html`). |
| **`<mime-mapping>`** | Indica al navegador el tipo de archivo que está recibiendo (si es una imagen, un PDF, un vídeo, etc.). |
| **`<servlet-mapping>`** | Mapea la ruta o "camino" (URL) que debe seguir una petición para ser procesada por el código Java. |

> ### etc/tomcat-users.xml👥🔑

Es `la base de datos de usuarios local de Tomcat`. Imagínalo como la "lista de invitados" donde apuntas quién tiene permiso para tocar la configuración del servidor.

- **Función Principal⚙️✅**

Se encarga de la `seguridad y el acceso.` Su trabajo es verificar que el nombre y la contraseña sean correctos para dejarte entrar a las herramientas de gestión (como el Manager App).


| Elemento | Qué configura |
| :--- | :--- |
| **`<role>`** | Define un tipo de permiso o "llave" (ej. `manager-gui` para usar la web de gestión). |
| **`<user>`** | Crea el perfil de una persona específica que podrá intentar hacer login. |
| **`username`** | El nombre de usuario que la persona tendrá que escribir para entrar. |
| **`password`** | La contraseña asociada a ese usuario (¡recuerda que se guarda en texto plano!). |
| **`roles`** | Es donde le asignas al usuario una o varias "llaves" (roles) de las que definiste antes. |


> ### etc/context.xml🔗🌍

Es el archivo que `define los recursos compartidos.` Imagínalo como una caja de herramientas que está en el pasillo del edificio: cualquier aplicación que viva allí puede salir, coger una herramienta (como una conexión a una base de datos) y usarla.

- **Función Principal⚙️✅**

Se encarga de `la configuración del entorno`. Su trabajo es definir parámetros y objetos (como fuentes de datos JDBC) que deben estar disponibles para todas las aplicaciones web de forma automática.


| Elemento | Qué configura |
| :--- | :--- |
| **`<Context>`** | Es el elemento raíz que envuelve toda la configuración del entorno. |
| **`<Resource>`** | Define recursos externos, como un "pool" de conexiones a una base de datos (MySQL, PostgreSQL, etc.). |
| **`<Parameter>`** | Crea variables de configuración que todas las aplicaciones pueden leer (ej. un correo de soporte). |
| **`<Manager>`** | Configura cómo se gestionan las sesiones (por ejemplo, para que no se pierdan al reiniciar el servidor). |
| **`<WatchedResource>`** | Indica a Tomcat qué archivos debe vigilar para reiniciar la app si detecta cambios (ej. el `web.xml`). |

> ### 🗺️ Mapa Visual de Arquitectura Tomcat

**server.xml (Configuración Maestra)**

  - └── tomcat-users.xml (Control de Accesos)

  - └── Entorno de Ejecución

     - ├── web.xml (Descriptor de Despliegue Global)

      -  └── context.xml (Recursos de Datos y Entorno)
