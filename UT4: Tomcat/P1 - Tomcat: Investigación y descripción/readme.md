> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web



![img](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Tomcat-Investigaci%C3%B3n%20y%20descripci%C3%B3n/logo.jpg)



> ### U.T. 4 **Práctica 1: Investigación y descripción de Tomcat 🐱**

**Curso:** 2ºDAW


**Autor:** Basi Córdoba Arcas

**Fecha:** 12/12/2025



> ### Investigación 🔍


> Catalina ⚙️🐱

Catalina es el `corazón de Tomcat.` Es el módulo que se encarga de cargar, gestionar y ejecutar tus aplicaciones web Java (servlets y JSPs). Piensa en él como el motor que hace funcionar la lógica de tu aplicación.

> Coyote 📡🔌

Es la parte que escucha en un `puerto` las solicitudes que vienen del navegador del usuario. Es como el front-end de red que comunica el exterior con el contenedor interno (Catalina).

> Jasper 🛠️📄

Jasper es el `traductor de Tomcat`. Cuando le llega una página JSP, la convierte en un código Java entendible por Catalina para que pueda ejecutarse. Se asegura de que las páginas dinámicas se sirvan correctamente.

> Manager 📑🕹️

Manager es el `panel de control` para tus aplicaciones web. Te deja subir, bajar o reiniciar tus war (archivos de aplicación) sin apagar Tomcat, lo cual es muy útil en producción.

> Host Manager 🌐🏠

Host Manager gestiona los `sitios web` dentro de Tomcat. Es donde puedes configurar si un solo servidor Tomcat va a alojar múltiples dominios o subdominios diferentes.


> bin 🚀📂
Contiene los archivos `"ejecutables"` necesarios para arrancar, detener y configurar el arranque del servidor.

> conf ⚙️📜
Es la carpeta de ajustes donde guardas los `archivos XML` que definen cómo se comporta Tomcat y sus usuarios.

> lib 📚📦
El `almacén de librerías (.jar)` que comparten todas tus aplicaciones para poder funcionar correctamente.

> logs 🗒️🔍
El registro donde se `guarda` todo lo que ocurre y donde debes mirar si algo falla (historial de errores).

> webapps 🌍🏗️
El lugar donde `"viven"` tus aplicaciones; cualquier carpeta o archivo .war aquí se convertirá en un sitio web.


 Flujo interno de funcionamiento 🔄📩

> Recepción de peticiones 🔄📩

Es la "portería" del servidor. Cuando alguien entra a tu web, este componente recibe el mensaje, traduce el idioma de internet (HTTP) al idioma de Java y prepara el paquete para pasárselo a los que trabajan dentro (Catalina).

> Contenedores 📥📦

En Tomcat, los contenedores son estructuras jerárquicas (Engine, Host, Context) que agrupan y organizan tus aplicaciones. Su función es aislar cada app para que lo que pase en una no afecte a las demás, garantizando seguridad y orden.

> Despliegue de Aplicaciones 🚀✨

Es el mecanismo automático que detecta, descomprime y activa tus programas para que estén disponibles en internet.
