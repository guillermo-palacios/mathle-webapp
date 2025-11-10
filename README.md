# 🧩 Mathle - Juego Web Full-Stack en Java

**Mathle** es una aplicación web full-stack, inspirada en "Wordle", que reta a los jugadores a resolver operaciones matemáticas. El proyecto está desarrollado íntegramente en **Java (Enterprise Edition)** y sigue una estricta arquitectura **Modelo-Vista-Controlador (MVC)**.

Este proyecto demuestra una implementación completa de un backend Java (con Servlets y JDBC) que se comunica con un frontend dinámico (JSP, CSS y JavaScript) y una base de datos relacional.



## 🏛️ Arquitectura: Modelo-Vista-Controlador (MVC)

El proyecto está diseñado para separar la lógica de negocio, la gestión de datos y la presentación al usuario.

* **Modelo (Model):**
    * **`data/dto` (Data Transfer Objects):** Clases puras de Java (`Usuario.java`, `Partida.java`) que representan los datos.
    * **`data/dao` (Data Access Objects):** La única capa que habla con la base de datos (`UsuarioDAO.java`, `PartidaDAO.java`). Contiene toda la lógica SQL para las operaciones CRUD.
    * **`data/common`:** Clases de utilidad para gestionar la conexión a la BBDD (`DBProperties.java`) y cargar consultas desde archivos `.properties`.

* **Vista (View):**
    * **`.jsp` (JavaServer Pages):** Archivos (ej: `vistaPartida.jsp`, `inicioSesion.jsp`) que renderizan el HTML dinámicamente.
    * **`css/` y `js/`:** Archivos estáticos que gestionan el estilo visual y la interactividad del frontend (ej: `estilosJuego.css`, `jugarPartida.js`).

* **Controlador (Controller):**
    * **`servlets/`:** Clases Java (`LoginServlet.java`, `PartidaServlet.java`) que actúan como el cerebro del backend.
    * Reciben peticiones HTTP del navegador (del frontend).
    * Llaman al Modelo (DAOs) para procesar la lógica.
    * Deciden qué Vista (JSP) mostrar al usuario.

## ✨ Características Principales

* **Aplicación Full-Stack:** Lógica de backend (Java) y frontend (JSP, CSS, JS) funcionales.
* **Gestión de Usuarios y Seguridad:** Sistema completo de registro e inicio de sesión. Las contraseñas se almacenan de forma segura en la base de datos usando *hashing* con **jbcrypt**.
* **Lógica de Juego:** Múltiples modos de juego, gestión de partidas y generación de problemas matemáticos.
* **Interactividad:** Ranking de partidas, chat de mensajes entre jugadores y personalización de temas (CSS).
* **Gestión de BBDD (DevOps):** Incluye scripts de Shell (`.sh`) para instalar, exportar e importar la base de datos **MariaDB**.

## 🛠️ Tecnologías Utilizadas

* **Backend:** Java (Servlets, JDBC)
* **Frontend:** JSP (JavaServer Pages), HTML, CSS, JavaScript
* **Base de Datos:** MariaDB (MySQL)
* **Gestión de Proyecto:** Apache Maven
* **Arquitectura:** MVC (Modelo-Vista-Controlador)
* **Seguridad:** jbcrypt (para hashing de contraseñas)
* **Servidor de Aplicaciones:** Apache Tomcat

## 🏃 Cómo Ejecutar el Proyecto

### 1. Configurar la Base de Datos

El proyecto requiere un servidor MariaDB (o MySQL).

1.  Dale permisos a los scripts de la BBDD:
    ```bash
    chmod +x *.sh
    ```
2.  (Si es necesario) Instala y configura el servidor MariaDB:
    ```bash
    sudo ./instalar_bbdd.sh
    ```
3.  Para cargar los datos dentro de la base de datos:
    ```bash
    sudo ./importar_bbdd.sh
    ```
4.  (Si es necesario) Para exportar los datos de la base de datos:
    ```bash
    sudo ./exportar_bbdd.sh
    ```

### 2. Compilar el Proyecto (con Maven)

Navega a la carpeta del proyecto Maven y usa `package` para crear el archivo `.war`.

```bash
cd mathle
mvn clean package
```
Esto generará el archivo `target/mathle.war`.

### 3. Desplegar en Apache Tomcat

1.  Asegúrate de que tienes Apache Tomcat 9 (o similar) instalado y ejecutándose.
    ```bash
    sudo systemctl start tomcat9
    ```
2.  Copia el archivo `.war` a la carpeta de despliegue de Tomcat:
    ```bash
    sudo cp target/mathle.war /var/lib/tomcat9/webapps/
    ```
3.  Tomcat detectará y desplegará automáticamente la aplicación.

### 4. ¡Jugar!

Abre tu navegador y ve a:
**`http://localhost:8080/mathle`**