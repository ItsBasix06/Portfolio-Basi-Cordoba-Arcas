> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web



![img](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Tomcat%3A%20Despliegue%20simple%20de%20una%20aplicaci%C3%B3n%20web/portada.jpg)



> ### U.T. 4 **Practica 3:  Despliegue simple de una aplicación web de Tomcat🚀🌐**

**Curso:** 2ºDAW


**Autor:** Basi Córdoba Arcas

**Fecha:** 23/01/2025


> ### 1. Descargar el WAR de internet🌐📥

Para poder descargarlo voy a abrir mi terminal y con `wget` descargare un war de internet, este es el war que he instalado:

```bash
wget https://tomcat.apache.org/tomcat-10.1-doc/appdev/sample/sample.war
```

![wget-war](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Tomcat%3A%20Despliegue%20simple%20de%20una%20aplicaci%C3%B3n%20web/wget-war.png)

> ### 2. Despliegue en la Carpeta webapps📂➡️


Una vez descargado la movemos con el comando `cp` a la carpeta de despliegue que es `tomcat10/webapps/` con el siguiente comando:
```bash
sudo cp ~/sample.war.1 /var/lib/tomcat10/webapps/sample.war
```
Y con ls -l comprobamos de que esta dentro de la carpeta.

####   Pasos que realiza Tomcat

| Fase | Acción Interna de Tomcat |
| :--- | :--- |
| **Detección** | Un hilo de ejecución llamado `HostConfig` escanea el directorio `webapps` periódicamente. Al encontrar un archivo `.war` nuevo, inicia automáticamente el proceso de despliegue. |
| **Descompresión** | Tomcat extrae el contenido del archivo WAR (proceso llamado *exploding*) y crea un directorio con el mismo nombre (ej. `/sample`) dentro de la misma carpeta. |
| **Carga de Contexto** | El servidor analiza el descriptor de despliegue (`WEB-INF/web.xml`) de la aplicación para configurar sus filtros, servlets y parámetros de inicio. |
| **Arranque** | Se instancian los componentes y la aplicación se marca como "activa", quedando lista para recibir peticiones en la URL correspondiente. |


> ### 3. Acceso a la Aplicacion💻🔓

Ahora vamos a probar si tenemos acceso a lo que nos hemos descargado por internet, abrimos nuestro navegador en mi caso `firefox`y ponemos la siguiente url -> `http://localhost:8080/sample/`

![navegador-ls](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Tomcat%3A%20Despliegue%20simple%20de%20una%20aplicaci%C3%B3n%20web/navegador-funcionamiento-ls.png)
