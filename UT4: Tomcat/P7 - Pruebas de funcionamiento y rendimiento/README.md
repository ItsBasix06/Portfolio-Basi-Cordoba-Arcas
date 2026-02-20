> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Pruebas%20de%20funcionamiento%20y%20rendimiento/logo.png)

> ### U.T. 4 **Practica 7: Pruebas de funcionamiento y rendimiento 🚀📈**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

> ### 1. Preparación y Prueba Base (Antes de optimizar) 🐢

Para realizar las pruebas de estrés a nuestro servidor Tomcat, voy a utilizar **ApacheBench** (`ab`), una herramienta de línea de comandos que permite lanzar miles de peticiones simultáneas para medir cómo responde el servidor. 

Primero, instalo la herramienta en mi máquina virtual Ubuntu:
```bash
sudo apt update
sudo apt install apache2-utils
```

Una vez instalada, lanzo mi **primera prueba de carga (Baseline)** contra la aplicación de prueba (`sample`) que tengo desplegada en el puerto 8080. Voy a simular **1.000 peticiones totales**, con **100 usuarios concurrentes** (accediendo a la vez):

```bash
ab -n 1000 -c 100 http://localhost:8080/sample/
```

**Resultados iniciales a destacar:**
Observo en la salida del comando las métricas principales, especialmente el *Time per request* (tiempo medio de respuesta) y el *Requests per second* (peticiones por segundo que es capaz de procesar con la configuración por defecto).

![prueba-base-apachebench](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Pruebas%20de%20funcionamiento%20y%20rendimiento/prueba-base-apachebench.png)

---

> ### 2. Ajustes de Rendimiento en `server.xml` 🛠️

Tomcat viene con una configuración conservadora para no consumir mucha RAM por defecto. Como en la prueba anterior el servidor se saturaba con facilidad, voy a modificar el archivo principal de configuración para asignarle más recursos.

Abro el archivo:
```bash
sudo nano /etc/tomcat10/server.xml
```

Busco el conector del puerto **8080** y le añado/modifico los siguientes parámetros para optimizar el manejo de hilos y conexiones:
* `maxThreads="500"`: Aumento el número máximo de hilos (usuarios simultáneos reales que Tomcat puede procesar a la vez).
* `acceptCount="500"`: Aumento el tamaño de la "sala de espera" (la cola) para las peticiones que llegan cuando todos los hilos están ocupados.
* `connectionTimeout="20000"`: Mantengo el tiempo de espera en 20 segundos para evitar que conexiones lentas bloqueen el servidor.

El bloque queda configurado así:

```xml
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443"
           maxParameterCount="1000"
           maxThreads="500"
           acceptCount="500" />
```

Guardo los cambios y reinicio el servicio para aplicar la nueva configuración:
```bash
sudo systemctl restart tomcat10
```

![configuracion-server-xml](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Pruebas%20de%20funcionamiento%20y%20rendimiento/configuracion-serve-conector.png)

---

> ### 3. Prueba Final y Comparativa (Después de optimizar) 🐇

Con el servidor recién configurado y con mayor capacidad para gestionar hilos, vuelvo a lanzar exactamente el mismo ataque con ApacheBench:

```bash
ab -n 1000 -c 100 http://localhost:8080/sample/
```

**Análisis y Comparativa:**
Al comparar los resultados de esta segunda prueba con los de la prueba base, noto una mejora significativa en el rendimiento:
1.  **Requests per second (Peticiones por segundo):** El número ha aumentado, lo que indica que Tomcat ahora es capaz de despachar más tráfico en el mismo periodo de tiempo.
2.  **Time per request (Tiempo por petición):** El tiempo medio que tarda un usuario en recibir su página ha disminuido al tener más hilos disponibles trabajando en paralelo.
3.  **Failed requests (Peticiones fallidas):** Gracias al aumento del `acceptCount`, el servidor rechaza menos conexiones en momentos de pico extremo.

![prueba-final-apachebench](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Pruebas%20de%20funcionamiento%20y%20rendimiento/prueba-final.png)
