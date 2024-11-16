content = """
# README - CI/CD Docker Compose Setup

Este archivo `docker-compose.yml` configura un entorno completo de CI/CD que incluye **Jenkins**, **SonarQube** y una base de datos **PostgreSQL** para el análisis de calidad de código.
---

## **Contenido**
1. [Servicios incluidos](#servicios-incluidos)
2. [Requisitos previos](#requisitos-previos)
3. [Configuración inicial](#configuración-inicial)
4. [Cómo ejecutar](#cómo-ejecutar)
5. [Detalles de configuración](#detalles-de-configuración)
6. [Notas adicionales](#notas-adicionales)

---

## **Servicios incluidos**
### **1. Jenkins**
- Imagen: `jenkins/jenkins:lts`
- **Descripción:** Jenkins es una herramienta de automatización utilizada para implementar pipelines de CI/CD.
- **Puertos expuestos:**
  - `8080`: Interfaz web de Jenkins.
  - `50000`: Comunicación con agentes esclavos de Jenkins.
- **Volúmenes:**
  - `jenkins_home`: Almacena la configuración y datos persistentes de Jenkins.
  - `/var/run/docker.sock`: Permite que Jenkins controle Docker en el host.

### **2. SonarQube**
- Imagen: `sonarqube:latest`
- **Descripción:** SonarQube es una herramienta para la calidad del código y análisis estático.
- **Puertos expuestos:**
  - `9000`: Interfaz web de SonarQube.
- **Configuración del entorno:**
  - Base de datos configurada en PostgreSQL.

### **3. PostgreSQL (DB)**
- Imagen: `postgres:latest`
- **Descripción:** Base de datos que respalda SonarQube.
- **Configuración del entorno:**
  - Usuario: `sonar`
  - Contraseña: `sonar`
  - Base de datos: `sonar`

---

## **Requisitos previos**
1. **Docker** y **Docker Compose** instalados en tu máquina.
   - [Instalar Docker](https://docs.docker.com/get-docker/)
   - [Instalar Docker Compose](https://docs.docker.com/compose/install/)
2. Puerto **8080**, **50000**, y **9000** disponibles en el host.

---

## **Configuración inicial**
1. **Persistencia de Jenkins:**
   - El volumen `jenkins_home` asegura que los datos de Jenkins no se pierdan al reiniciar el contenedor.
2. **Acceso a Docker desde Jenkins:**
   - La vinculación de `/var/run/docker.sock` permite que Jenkins administre contenedores Docker en el host.

3. **Base de datos PostgreSQL:**
   - Preconfigurada con credenciales y base de datos necesarias para SonarQube.

---

## **Cómo ejecutar**
1. Clona el repositorio que contiene este archivo `docker-compose.yml` o crea uno.
2. Navega al directorio donde se encuentra el archivo.
3. Ejecuta el siguiente comando:
   ```bash
   docker-compose up -d
