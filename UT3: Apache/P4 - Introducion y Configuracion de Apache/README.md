
> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web



![img](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/Apache.png)




> ### U.T. 2 **Práctica 1: Apache**

**Curso:** 2ºDAW


**Autor:** Basi Córdoba Arcas

**Fecha:** 07/11/2025



> ## INDICE

**1. Descargar Apache**

**2. Creacion de nuestro sitio web**

**3. Configuración del archivo de configuración en Virtualhost**

**4. Activacion del archivo VirtualHost**

**5. Comprobacion en el navegador**


> ## INTRODUCCION

En esta practica vamos a instalar y configurar el servidor Apache.

> #### ¿Que es Apache?

El servidor web Apache, también conocido como Apache HTTP Server, es un software desarrollado por la Apache Software Foundation.

Es un servidor web de código abierto, lo que significa que su código fuente está disponible para que cualquiera lo estudie, modifique y mejore.

> #### ¿Para qué Sirve Apache?

Apache se utiliza principalmente para alojar sitios web en internet. Algunas de las funciones principales de Apache incluyen:

**1. Alojar sitios web**

**2. Gestión de conexiones**

**3.Soporte para módulos**

**4.Configuración flexible**


> ## DESARROLLO

> ### 1. Descargar Apache

En la terminal actualizamos los paquetes a la ultima version con **sudo apt update** y luego procederemos a instalar el servidor Apache con **sudo apt install Apache2**:

![descarga-apache](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/DescargarApache.png)

Ahora comprobamos en cualquier navegador sobre si funciona correctamente el servidor Apache2, yo usare el predeterminado de ubuntu **(Firefox)** y este es el resultado:


![comprobacion](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/comprobar-web-apache.png)

> ### 2. Creacion de nuestro sitio web

Ahora para poder crear nuestro primer sitio web de Apache hay que crear carpetas para crear el sitio, por ello con **mkdir** creamos en esta ruta los siguiente: **sudo mkdir /var/www/gci/** y luego nos movemos a la carpeta con **cd** y despues usamos **nano** para crear un nuevo fichero llamado **index.html**:

![movimiento](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/Creacion-carpetas-movimiento-creacionfichero.png)

Ponemos un mensaje dentro en el titulo diciendo **Ubuntu ese lo mejor** y en un parrafo ponemos otro mensaje diciendo que **estoy corriendo esta web en ubuntu server**:

![fichero](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/contenido-fichero-apache.png)

> ### 3. Configuración del archivo de configuración en Virtualhost


Ahora nos dirigimos a la siguiente ruta: **cd /etc/apache2/sites-available/**
y con cp **(copiar)** copiamos lo que vino instalado por defecto con apache que es un virtualhost y lo pegamos en un nuevo fichero llamado **gci.conf** y entramos con nano:

![configuracion-entrar](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/movemosrutaapache-copiar-fichero.png)

-Una vez dentro cambiamos la linea de mail ponemos mi correo electronico, despues en la ruta en **DocumentRoot** la cambiamos en nuestro casso a **/var/www/gci/** y el nombre del servidor ponemos **gci.example.com**:

![email-server](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/correo-ruta-y-nombre-apache.png)

> ### 4. Activacion del archivo VirtualHost

Ahora tenemos que activar el archivo de configuracion de hosts virtuales para habilitarlo,por ello escribimos el siguiente comando **sudo a2ensite gci.conf** y nos pedira recargar el servicio apache2 con **systemctl reload apache2** y con status vemos que funciona sin problemas: 

![comprobamos-habilitar](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/habilitarHosts-reload-status.png)
### 5. Comprobacion en el navegador
Ahora nos dirigimos en el navegador a poner nuestro nombre de host para ver si nuestro mensasje que pusimos funciona con **gci.example.com** pero da un error,aparece esto:

![error-apache](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/error-no-funciona-apache.png)

-La solucion mas efectiva es abrir el fichero /etc/hosts y añadir una nueva linea que cuando te conectes al ordenador detecte el nombre de nuestro servidor **gci.example.com**:

![etc-hosts](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/etc-hosts-cambio-nombre.png)

Comprobamos el acceso antes de nada reiniciamos con reload el servicio de apache y veamos en el navegador:

![comprobar-correcto](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UT2%3A%20Introducci%C3%B3n%20a%20las%20Aplicaciones%20WEB/img/comprobacion-funcionamiento-funciona.png)


> ## Resultados y Conclusiones

### ¿Que hemos conseguido?

He conseguido a poder poner en marcha y funcionamiento el servicio Apache de forma basica donde podemos ver que en cualquier navegador aparece mi mensaje personalizado que yo mismo configure y una documentacion del proceso de descarga, instalacion e configuracion de Apache


### Conclusiones
Para mí, Apache es un servidor web muy útil y fácil de usar. Me gusta porque es fiable, compatible con muchos lenguajes y me ha ayudado a entender cómo funciona un servidor de verdad.

> ## Bibliografia

He usado los siguientes enlaces para documentar la practica.

> [Documentacion de Ubuntu](https://ubuntu.com/tutorials/install-and-configure-apache#1-overview)
