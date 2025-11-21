# Iniciacion a la Virtualización
> ### Instalacion de Ubuntu Desktop 24.04 LTS 
Ya he instalado **ubuntu desktop** y agregado la extension de **Guest Additions** para mayor compatibilidad ya sea carpetas, pantalla completa,etc...
La **red** la tengo en modo adaptador puente para tener conexion a internet con la maquina anfitrión,el resultado es este:

> ![ubuntu-destop](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UD1%3A%20GitHub%20y%20MarkDown/img/P3%20-%20Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/Ubuntu-desktop.png)

> ## Instalacion de Docker en Ubuntu
Un **contenedor** es una unidad de software que incluye todo lo necesario para ejecutar una aplicación.  
A diferencia de una máquina virtual, comparte el kernel del sistema operativo, por lo que es más ligero y rápido.

-Las **principales ventajas** de Docker son su **portabilidad, aislamiento, escalabilidad y rapidez de despliegue.**

> #### 1.Actualizo los respositorios con  (sudo apt update && sudo apt upgrade -y)
Procedo a hacer los dos comandos que aparecen,el sudo apt update y sudo apt upgrade para actualzar los repositorios en ubuntu antes de ponernos.

> #### 2.Se instalan las dependencias (sudo apt install ca-certificates curl gnupg -y)
Se instalan tres paquetes esenciales que se suelen necesitar antes de añadir repositorios externos o instalar software desde fuentes seguras.

> #### 3.Añade el repositorio de Docker e instala Docker Desktop (curl -fsSL https://get.docker.com | sudo sh, sudo apt install docker-desktop -y)
Este comando instala Docker Engine, Docker CLI, y containerd automáticamente en el sistema para que funcione correctamente.

> #### 4.Verifica que Docker funciona correctamente:
Una vez instalado, ponemos una imagen donde se ve claramente su version especifica y que funciona el primer programa con el tipico HolaMundo (Usar sudo sino no va xd)

> ![funcionamiento](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UD1%3A%20GitHub%20y%20MarkDown/img/P3%20-%20Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/holamundo-docker.png)


> ## Instalación en Docker

> ### Buscar imágenes disponibles

> docker search nginx

> docker search tomcat

Es como si fuera una tienda o repositorio publico

> ### Descargar e iniciar contenedores:

 docker run -d -p 8080:80 --name webserver nginx

 docker run -d -p 8081:8080 --name appserver tomcat

 Para ejecutar los contenedores pondremos el comando que se ha puesto arriba ^^

 > ![descargar-contenedores-nginx](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UD1%3A%20GitHub%20y%20MarkDown/img/P3%20-%20Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/Descargar-Contenedor-nginx.png)


> ![descargar-contenedores-tomcat](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UD1%3A%20GitHub%20y%20MarkDown/img/P3%20-%20Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/Descargar-Contenedor-tomcat.png)

> ## Funcionamiento en el navegador (localhost)

Comprobamos el funcionamiento de cada uno mediante localhost con sus puertos y tambien compruebo de que estan activos

 ![comprobacion-navegador](https://raw.githubusercontent.com/ItsBasix06/Porfolio-Basi-Cordoba-Arcas/refs/heads/main/UD1%3A%20GitHub%20y%20MarkDown/img/P3%20-%20Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/comprobar-estado-y-funcionamiento-web.png)
