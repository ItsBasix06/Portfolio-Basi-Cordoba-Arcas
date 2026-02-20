> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/contenedores%20(Docker)/logo.jpg)

> ### U.T. 4 **Practica 8: Tomcat en contenedores (Docker) 🐳📦**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

> ### 1. Descarga de la Imagen Oficial (Docker Pull) ⬇️

En esta práctica cambiamos radicalmente la forma de despliegue. En lugar de instalar Tomcat en nuestro sistema operativo base, vamos a utilizar una versión "empaquetada" y aislada en un contenedor Docker.

El primer paso es obtener la "plantilla" (imagen) oficial de Tomcat desde el repositorio público Docker Hub. Ejecuto el siguiente comando en la terminal:

```bash
sudo docker pull tomcat:latest
```

Docker se encarga de descargar las capas necesarias (un sistema Linux base, el JDK de Java y el propio servidor Tomcat preinstalado).

![terminal-docker-pull](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/contenedores%20(Docker)/terminal-docker-pull.png)

---

> ### 2. Preparación del Entorno Local para el Despliegue 📂

El objetivo es que el Tomcat del contenedor ejecute **nuestra** aplicación web, no las que trae por defecto. Para ello, usaremos una técnica llamada "Montaje de Volumen", que consiste en conectar una carpeta de mi máquina anfitriona (Ubuntu) con la carpeta de despliegue dentro del contenedor.

Primero, necesito preparar esa carpeta local. Voy a crear un directorio llamado `mis-apps-docker` en mi carpeta personal y copiaré allí el archivo `sample.war` (que he usado en prácticas anteriores):

```bash
# 1. Me aseguro de estar en mi carpeta personal
cd ~

# 2. Creo la carpeta que servirá de "puente"
mkdir mis-apps-docker

# 3. Copio la aplicación de prueba a esa carpeta
# (Asumo que sample.war está en la carpeta donde estoy actualmente, si no, ajusta la ruta origen)
cp sample.war ~/mis-apps-docker/

# 4. Verifico que el archivo está ahí
ls -l ~/mis-apps-docker/
```

Ahora, mi carpeta local `~/mis-apps-docker` contiene el `.war` listo para ser inyectado en el contenedor.

![terminal-preparacion-carpeta](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/contenedores%20(Docker)/terminal-preparacion.png)

---

> ### 3. Arranque del Contenedor con Montaje de Volumen (Docker Run) 🚀

Este es el paso crucial. Voy a arrancar el contenedor con un comando que hace varias cosas a la vez:

1.  **`-d` (Detached):** Ejecuta el contenedor en segundo plano.
2.  **`--name mi-tomcat`:** Le da un nombre fácil para identificarlo.
3.  **`-p 8081:8080` (Mapeo de puertos):** Importante. Como ya tengo un Tomcat nativo usando el puerto 8080 en mi máquina, le digo a Docker que el puerto 8080 *del contenedor* sea accesible a través del puerto **8081** de mi máquina física.
4.  **`-v ~/mis-apps-docker:/usr/local/tomcat/webapps` (Volumen):** La magia. "Engancha" mi carpeta local `~/mis-apps-docker` directamente en la ruta donde Tomcat busca las aplicaciones dentro del contenedor (`/usr/local/tomcat/webapps`).

Ejecuto el comando:

```bash
sudo docker run -d --name mi-tomcat -p 8081:8080 -v ~/mis-apps-docker:/usr/local/tomcat/webapps tomcat:latest
```

Para verificar que ha arrancado y ha detectado la aplicación, reviso los logs:

```bash
sudo docker logs mi-tomcat
```

![terminal-docker-run-logs](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/contenedores%20(Docker)/terminal-docker-logs.png)

---

> ### 4. Verificación del Despliegue en el Navegador ✅

Si el montaje del volumen ha funcionado, Tomcat habrá descomprimido automáticamente el `sample.war` que pusimos en la carpeta compartida. Accedo al navegador usando el puerto nuevo que he definido (8081):

URL: `http://localhost:8081/sample/`

La aplicación carga correctamente, confirmando que el contenedor está sirviendo los archivos de mi máquina local.

![navegador-sample-docker](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/contenedores%20(Docker)/navvegador-sample.png)

---

> ### 5. Diferencias: Tomcat Nativo vs. Tomcat en Contenedor 🆚

Tras haber trabajado con ambos métodos de despliegue durante este curso, resumo las principales diferencias en esta tabla comparativa:

| Característica | Tomcat Nativo (Instalación tradicional con `apt`) | Tomcat en Contenedor (Docker) |
| :--- | :--- | :--- |
| **Instalación y Entorno** | Compleja. Requiere instalar Java (JDK), configurar variables de entorno, usuarios y permisos en el S.O. anfitrión. Depende de las versiones de librerías del sistema. | Inmediata (`docker run`). Todo viene preinstalado y configurado dentro de la imagen. El entorno es siempre idéntico. |
| **Aislamiento** | Bajo. Tomcat comparte recursos directamente con el sistema operativo. Un fallo grave o una mala configuración de seguridad podría afectar al servidor completo. | Alto. Se ejecuta en un entorno aislado (sandbox). Sus procesos y sistema de archivos están separados del host. |
| **Portabilidad** | Baja. "Funciona en mi máquina". Mover la configuración a otro servidor requiere repetir pasos manuales y asegurar que el entorno sea idéntico. | Muy alta. La imagen Docker garantiza que funciona exactamente igual en desarrollo, pruebas y producción, sin importar el S.O. subyacente. |
| **Actualizaciones** | Tediosas. Hay que gestionar repositorios, dependencias de Java y posibles conflictos al actualizar. | Sencillas. Basta con usar una versión más nueva de la imagen (`tomcat:11-jdk17`) y volver a lanzar el contenedor. |
| **Ubicación de Apps** | Las aplicaciones residen físicamente en `/var/lib/tomcat/webapps` del servidor. | Las aplicaciones se suelen "inyectar" mediante volúmenes (como en esta práctica) o se copian dentro al crear una imagen personalizada. |
| **Gestión de Puertos** | Usa directamente los puertos del host (ej. 8080). Si está ocupado, hay que editar `server.xml`. | Los puertos internos se mapean externamente (`-p 8081:8080`), permitiendo ejecutar múltiples Tomcats sin conflictos. |

---

> ### 6. Opcional: Nota sobre Despliegue en la Nube ☁️

El uso de Docker estandariza tanto el despliegue que hacerlo en la nube (AWS EC2, Azure VM, Google Cloud) es prácticamente idéntico a hacerlo en local:

1.  Se contrata una máquina virtual básica (IaaS) en el proveedor de la nube.
2.  Se instala Docker en esa máquina remota.
3.  Se sube el archivo `.war` y se ejecuta exactamente el mismo comando `docker run...` que hemos usado en el paso 3.

Al estar contenierizado, no importa si la máquina subyacente está en mi casa o en un centro de datos de Amazon; el comportamiento del Tomcat será el mismo.
