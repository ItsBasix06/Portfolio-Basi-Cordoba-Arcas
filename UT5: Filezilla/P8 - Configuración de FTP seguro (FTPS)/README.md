> # DESARROLLO DE APLICACIONES WEB
> ### Despliegue de Aplicaciones Web

![portada](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Configuraci%C3%B3n%20de%20FTP%20seguro%20(FTPS)/logo.jpg)

> ### U.T. 5 **Actividad 8: Configuración de FTP seguro (FTPS) 🔒🔑**

**Curso:** 2ºDAW

**Autor:** Basi Córdoba Arcas

**Fecha:** 20/02/2026

---

### 1. Generación del Certificado TLS

Para habilitar el cifrado, es necesario contar con un certificado digital. En FileZilla Server, he generado un **certificado auto-firmado** siguiendo estos parámetros:
* **Tipo de llave:** Ed25519 (o RSA 4096 bits).
* **Common Name (CN):** `localhost` o la IP del servidor.
* **Función:** Este certificado permitirá cifrar tanto el canal de control (comandos/contraseñas) como el de datos (archivos).

![captura-generacion-certificado](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Configuraci%C3%B3n%20de%20FTP%20seguro%20(FTPS)/captura-generacion-certificado.png)

---

### 2. Configuración de FTPS Explícito Obligatorio 🛠️

Para garantizar que ningún usuario se conecte de forma insegura, se ha configurado el servidor para que rechace conexiones que no utilicen TLS:

1.  **Protocolo:** Se ha seleccionado la opción **"Require explicit FTP over TLS"** en la configuración de los *listeners*.
2.  **Seguridad:** Esto obliga al cliente a enviar el comando `AUTH TLS` antes de que el servidor acepte cualquier credencial.

![captura-configuracion-segura](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Configuraci%C3%B3n%20de%20FTP%20seguro%20(FTPS)/seguridad-lts.png)

---

### 3. Verificación del Cifrado en el Cliente 🧪

He realizado una conexión desde FileZilla Client para verificar que el túnel seguro está activo:

* **Certificado:** Al conectar, el cliente muestra una ventana emergente con los detalles del certificado generado.
* **Icono de Seguridad:** Se observa un icono de un **candado cerrado** en la barra de estado inferior.
* **Mensaje de Log:** El cliente confirma: `Estado: Conexión TLS establecida.`.

![captura-verificacion-ftps](https://raw.githubusercontent.com/ItsBasix06/Portfolio-Basi-Cordoba-Arcas/refs/heads/main/UT5%3A%20Filezilla/img/Configuraci%C3%B3n%20de%20FTP%20seguro%20(FTPS)/captura-verificacion-ftps.png)

---

### 4. Conclusión sobre Seguridad

Gracias a la implementación de FTPS, toda la información que viaja entre el cliente y el servidor (incluyendo el nombre de usuario y la contraseña) está protegida contra ataques de tipo *Sniffing* (escucha de red). Sin esta configuración, las credenciales viajarían en texto claro, comprometiendo la seguridad del servidor.
