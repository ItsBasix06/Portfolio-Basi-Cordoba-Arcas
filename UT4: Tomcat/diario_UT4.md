> # Diario de la Unidad Didáctica 4: Tomcat

> ## Qué he aprendido

En esta unidad he entendido la diferencia entre un servidor web tradicional (como Apache) y un contenedor de servlets/JSP como Tomcat, que está pensado para ejecutar aplicaciones hechas en Java. 

He aprendido que Tomcat no funciona por sí solo, sino que necesita tener instalado el JDK (Java Development Kit) y que es vital configurar correctamente las variables de entorno como `JAVA_HOME` y `CATALINA_HOME`. 
También he descubierto cómo desplegar aplicaciones empaquetadas en archivos `.war` y cómo dar permisos editando el archivo `tomcat-users.xml` para poder acceder al panel de administración (*Manager App*).

> ## Qué no entiendo

Todavía me cuesta un poco diferenciar para qué sirve exactamente cada archivo de configuración XML (`server.xml`, `web.xml`, `context.xml`...). A veces dudo en cuál de ellos tengo que meter mano para hacer un cambio concreto. 
También se me hace un poco lioso el tema de conectar Apache normal con Tomcat usando el conector AJP o proxy inverso para que trabajen juntos.

> ## Qué me ha gustado

Me ha gustado mucho usar la interfaz web del *Manager App*. Es súper visual y cómodo poder subir un archivo `.war` desde el navegador, darle a un botón y ver cómo se despliega y arranca la aplicación automáticamente. 
También mola bastante la satisfacción de entrar a `localhost:8080` y ver la página inicial del gatito de Tomcat cuando por fin logras que arranque bien.

> ## Qué no me ha gustado

Pelearme con las variables de entorno de Windows me pareció bastante pesado; si te equivocas en una sola letra de la ruta, el servidor simplemente no arranca. 
Tampoco me gustan los mensajes de error de Java ("stack traces"). Cuando algo falla, suelta unos bloques de texto larguísimos en los logs que al principio asustan y son difíciles de descifrar.

> ## Conclusión

Esta unidad me ha enseñado que el ecosistema de Java requiere ser mucho más estricto y ordenado con las versiones y las rutas que otros servidores. Aunque Tomcat impone un poco de respeto al principio por la cantidad de archivos XML que tiene, una vez que le pillas la lógica a su estructura de carpetas y al despliegue, te das cuenta de que es una herramienta súper potente para aplicaciones pesadas.
