# Informe de Práctica: Automatización del Despliegue de una Aplicación Backend con Docker y PostgreSQL
## 1. Título
Automatización del Despliegue Local de una Aplicación Backend en Java utilizando Docker, Docker Compose, PostgreSQL y pgAdmin.
## 2. Tiempo de Duración
120 minutos (incluyendo instalación, configuración, depuración de errores y verificaciones finales).
## 3. Fundamentos
Las bases de esta labor se centran en empaquetar y coordinar programas informáticos usando Docker, una herramienta libre que permite meter aplicaciones junto a todo lo que necesitan en cajitas separadas, livianas y fáciles de mover. Docker soluciona líos típicos al desarrollar y lanzar software, como el fallo de "en mi equipo funcionaba bien pero en producción no", al meter todo en plantillas fijas que andan igual en cualquier sistema con Docker instalado.
Un contenedor Docker es la versión activa de una imagen, que es en sí un paquete con el código del programa, las librerías, utilidades y ajustes requeridos. El modo de operar de Docker depende de un servidor central (el motor) que maneja los contenedores a través de un medio de comunicación, usando apartados y límites de recursos de Linux para mantenerlos aislados. En Windows y Mac, Docker Desktop usa una máquina virtual liviana para imitar esto. Esta organización facilita crecer, ya que los contenedores comparten el núcleo del sistema principal pero mantienen su separación en cuanto a procesos, archivos y conexiones.
Docker Compose amplía Docker al posibilitar describir y levantar aplicaciones con varios contenedores usando un documento YAML específico. Esto abarca servicios (los contenedores), espacios para guardar información de forma permanente (evitando que se borre al reiniciar) y redes hechas a medida para que se hablen entre ellos. Por ejemplo, en este ejercicio, se crea una red llamada "app-network" para unir PostgreSQL, pgAdmin y la aplicación del lado del servidor, asegurando que se puedan comunicar sin abrir puertos al exterior sin necesidad.
PostgreSQL es un sistema libre para manejar bases de datos ordenadas, potente y ajustable, que soporta el lenguaje SQL estándar y opciones avanzadas como índices de datos JSON y transacciones seguras (ACID). Al estar en contenedores, se configura con claves específicas para el usuario, la clave secreta y el nombre de la base de datos, y se usan volúmenes para guardar los datos en su ubicación habitual. pgAdmin es una interfaz gráfica por web para administrar PostgreSQL, permitiendo conectarse, ejecutar consultas y ver su estado visualmente.
Un método importante es la construcción en varias fases dentro de los Dockerfiles, que hace que las plantillas sean más pequeñas al separar las partes: una para armar el código (con herramientas pesadas como Maven si es Java) y otra para ejecutar (súper ligera, solo con el resultado final como un archivo JAR). Esto reduce el tamaño de la plantilla (de mucha memoria a unos 100MB), mejora la seguridad (no dejando el código fuente a la vista) y agiliza el lanzamiento. En el caso de Java con Spring Boot, se usa Maven para construir y Eclipse Temurin como base para el JDK/JRE.
Esta conexión automática hace que el lanzamiento en el equipo local sea simple, promoviendo el trabajo constante y las pruebas. Las ventajas incluyen que siempre funciona igual, que las dependencias no estorban y que es fácil aumentar la capacidad para el entorno final (por ejemplo, usando Kubernetes).
## 4. Conocimientos previos.
Para realizar esta práctica, el estudiante necesita tener claros los siguientes temas:
- Comandos básicos de Linux/Unix (ls, cd, mkdir, etc.).
- Manejo de terminal o Git Bash en Windows.
- Conceptos básicos de Git (clonar repositorios).
- Fundamentos de bases de datos relacionales (SQL, tablas, conexiones).
- Programación en Java y manejo de Maven (para compilar proyectos Spring Boot).
- Nociones básicas de redes y puertos (TCP/IP).
- Entendimiento de variables de entorno y archivos de configuración (.env, YAML).
## 5. Objetivos a Alcanzar
- Implementar contenedores para PostgreSQL y pgAdmin con volúmenes y redes para persistencia y conectividad.
- Crear una imagen Docker optimizada para una aplicación backend en Java utilizando multi-stage builds.
- Configurar Docker Compose para orquestar múltiples servicios y asegurar la conexión entre la app y la base de datos.
- Verificar el despliegue local y la funcionalidad de la aplicación, incluyendo persistencia de datos y logs.
## 6. Equipo Necesario
- Computador con sistema operativo Windows, Linux o Mac (con al menos 4GB RAM y procesador dual-core).
- Instalación de Docker Desktop (versión 4.0 o superior).
- Git Bash o terminal equivalente.
- Navegador web (Chrome, Firefox) para acceder a pgAdmin.
- Acceso a internet para descargar imágenes Docker y clonar el repositorio.
## 7. Material de Apoyo
- Documentación oficial de Docker: https://docs.docker.com/.
- Documentación de PostgreSQL: https://www.postgresql.org/docs/.
- Documentación de pgAdmin: https://www.pgadmin.org/docs/.
- Guía de Spring Boot con Docker: https://spring.io/guides/gs/spring-boot-docker/.
- Cheat sheet de comandos Docker: https://dockerlabs.collabnix.com/docker/cheatsheet/.
- Repositorio base del proyecto: https://github.com/maguaman2/tendencias-mar22-security.git.
## 8. Procedimiento
### Paso 1: Preparación del entorno. 
Clona el repositorio con git clone https://github.com/maguaman2/tendencias-mar22-security.git y navega a la carpeta. Instala Docker si no está presente.
### Paso 2: Configura la base de datos. 
Crea docker-compose.yml con servicios para PostgreSQL y pgAdmin, incluyendo volúmenes y redes. Crea .env con variables como usuario y contraseña.
### Paso 3: Levanta los servicios de BD. 
Ejecuta docker-compose up -d y verifica con docker ps.
### Paso 4: Crea el Dockerfile. 
Define un multi-stage build con Maven para compilar la app Java y una etapa runtime ligera.
### Paso 5: Construye la imagen. 
Ejecuta docker build -t mi-app-backend:latest ..
### Paso 6: Integra la app en Docker Compose.
Agrega el servicio backend al docker-compose.yml con variables para conectar a PostgreSQL.
### Paso 7: Despliega todo. 
Ejecuta docker-compose up -d --build y verifica logs y conexiones.
## 9. Resultados Esperados
Hay que verificar que los recintos de PostgreSQL, pgAdmin y la aplicación del lado del servidor arranquen sin problemas, logrando que esta última se enlace con la base de datos y conteste en el puerto designado (por ejemplo, 8081). La información se guarda de forma permanente mediante discos virtuales, y pgAdmin facilita realizar consultas a través de la interfaz gráfica. En los registros, se aprecian notificaciones de que la conexión fue buena y de que la aplicación ya empezó a funcionar. Las imágenes capturadas evidenciarían los contenedores usando docker ps, la pantalla de pgAdmin y los mensajes generados por Spring Boot.
## 10. Bibliografía
- Merkel, D. (2014). Docker: lightweight linux containers for consistent development and deployment. Linux Journal, 2014(239), 2.
- PostgreSQL Global Development Group. (2023). PostgreSQL Documentation. Retrieved from https://www.postgresql.org/docs/
- pgAdmin Development Team. (2023). pgAdmin Documentation. Retrieved from https://www.pgadmin.org/docs/