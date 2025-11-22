> # Diario de la Unidad Didáctica 2: Despliegue Web

> ## Qué he aprendido

En esta unidad he entendido por fin la diferencia entre un cliente y un servidor FTP. También me ha quedado claro cómo funcionan los modos activo y pasivo y para qué sirven los puertos 20 y 21.

En cuanto a la instalación de Apache, he visto dos formas muy distintas de hacerlo. En Windows es un proceso más manual, ya que hay que instalar librerías Visual C++ y modificar el archivo `httpd.conf`. En cambio, en Ubuntu Server todo es mucho más sencillo: basta con usar un par de comandos desde la terminal para tener Apache funcionando.

Además, he aprendido conceptos básicos de seguridad, como configurar el firewall con UFW y entender cómo funcionan los permisos con `chmod` y `chown`.

> ## Qué no entiendo

A pesar de los avances, todavía tengo dudas con los **Virtual Hosts**. Sé para qué sirven, pero me lío cuando intento configurar varios sitios web en una misma IP sin provocar conflictos.

Los **permisos numéricos** también me confunden un poco. Sé que `755` y `644` son los más comunes, pero aún no tengo claro cuándo usar cada uno exactamente.

> ## Qué es lo que más me ha gustado

Lo que más me ha gustado ha sido la satisfacción de poner `localhost` en el navegador y ver que todo funciona. Ese momento en el que el servidor responde te hace sentir que todo el esfuerzo ha valido la pena.

Otra cosa que me ha encantado es trabajar desde la terminal. Usar comandos como `systemctl` me ha hecho sentir que controlo el sistema de una forma más profesional.

> ## Lo que menos me ha gustado

La instalación en Windows ha sido lo peor. Todo es más manual, más lento y más delicado, sobre todo comparado con la facilidad con la que se hace en Linux.

También ha sido frustrante tener que resolver los típicos problemas de puertos ocupados, especialmente con el famoso puerto 80.

> ## Conclusión

En general, esta unidad me ha demostrado que Linux es una opción mucho más eficiente para gestionar servidores. Apache me parecía algo complicado al principio, pero ahora veo que es una herramienta muy lógica una vez entiendes sus bases.
