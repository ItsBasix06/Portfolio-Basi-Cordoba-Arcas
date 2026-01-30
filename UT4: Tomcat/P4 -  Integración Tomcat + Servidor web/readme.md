> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web



![img](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Integraci%C3%B3n%20Tomcat%20%2B%20Servidor%20web/logo.jpg)



> ### U.T. 4 **Practica 4: Integración Tomcat + Servidor web🤝🔗**

**Curso:** 2ºDAW


**Autor:** Basi Córdoba Arcas

**Fecha:** 30/01/2026

> ### 1. Instalacion de Apache en Ubuntu Desktop🖥️📦


Primero antes de instalar Apache haremos un `sudo apt update` para actualizar los paquetes y luego un `sudo apt install apache2` quedandose asi:

```bash
sudo apt update
sudo apt install apache2
```

En mi caso Apache2 ya estaba instalado en mi sistema y contiene la ultima version:

![apache-inst](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Integraci%C3%B3n%20Tomcat%20%2B%20Servidor%20web/instalar-apache.png)


> ### 2. Configurar el Reverse Proxy🛡️➡️

Para que apache pueda asi decirlo **"hablar"** con Tomcat necesita instalar unos `moddulos`, usaremos el metodo Reverse Proxy pienso que es mas compatible y moderno:

```bash
sudo a2enmod proxy
sudo a2enmod proxy_http
```

![activar-mod](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Integraci%C3%B3n%20Tomcat%20%2B%20Servidor%20web/activar-modulos.png)

Y luego hay que reiniciar el servicio de Apache con `systemctl restart apache`.

#### **Configuracion de la "redirección"**

Tenemos que decirle a Apache que todo lo que llegue a una ruta específica `lo envíe` a Tomcat. Vamos a editar el archivo que fue creado por apache al instalarse por defecto:

```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

#### **Agregar las directivas de Proxy"**

Ahora una vez dentro del fichero de configuracion, hay que agregar 3 lineas, las agregare justo debajo de donde pone `DocumentRoot /var/www/html`

```bash
ProxyPreserveHost On
ProxyPass /sample http://localhost:8080/sample
ProxyPassReverse /sample http://localhost:8080/sample
```
![3lineas-agre](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Integraci%C3%B3n%20Tomcat%20%2B%20Servidor%20web/3lineas-agregadas.png)

Eso quiere decir que si  alguien pone en la barra de busqueda `/sample`, se dirige puerto 8080 de Tomcat, lo busca y se lo da al usuario.

Una vez hecho guardamos con `Control + O` y salimos con `Control + X` y procedemos a reiniciar de nuevo el servidor de apache con `systemctl restart apache`.

> ### 3. Verificacion del funcionamiento de la aplicacicon web🌐✅


#### 1. Acceso directo (Tomcat) 

Entramos en el navegador directamente con el puerto 8080 para ver si funciona que es `http://localhost:8080/sample/`

![8080-funcionamiento](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Integraci%C3%B3n%20Tomcat%20%2B%20Servidor%20web/funcionamiento-web-8080.png)


Como pueden ver funciona correctamente en el puerto 8080.


#### 2. Acceso integrado (Apache + Tomcat)
 
Ahora comprobemos lo que pasaria si lo ponemos sin el puerto 8080, es decir la url asi y sale igual que antes (tuve un problemilla de compatbilidad por el navegador ya que siempre por defecto me ponia como `https` pero ya esta solucionado:

![sin8080-funcionamiento](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT4%3A%20Tomcat/img/Integraci%C3%B3n%20Tomcat%20%2B%20Servidor%20web/funcionamiento-web-sin8080.png)


