# README - CI/CD Docker Compose Setup

This `docker-compose.yml` file sets up a complete CI/CD environment that includes **Jenkins**, **SonarQube**, and a **PostgreSQL** database for code quality analysis.
---

## **Table of Contents**
1. [Included Services](#included-services)
2. [Prerequisites](#prerequisites)
3. [Initial Setup](#initial-setup)
4. [How to Run](#how-to-run)
5. [Configuration Details](#configuration-details)
6. [Additional Notes](#additional-notes)

---

## **Included Services**
### **1. Jenkins**
- Image: `jenkins/jenkins:lts`
- **Description:** Jenkins is an automation tool used to implement CI/CD pipelines.
- **Exposed Ports:**
  - `8080`: Jenkins web interface.
  - `50000`: Communication with Jenkins agent nodes.
- **Volumes:**
  - `jenkins_home`: Stores Jenkins configuration and persistent data.
  - `/var/run/docker.sock`: Allows Jenkins to manage Docker on the host.

### **2. SonarQube**
- Image: `sonarqube:latest`
- **Description:** SonarQube is a tool for code quality and static analysis.
- **Exposed Ports:**
  - `9000`: SonarQube web interface.
- **Environment Configuration:**
  - Configured to use the provided PostgreSQL database.

### **3. PostgreSQL (DB)**
- Image: `postgres:latest`
- **Description:** Database backend for SonarQube.
- **Environment Configuration:**
  - User: `sonar`
  - Password: `sonar`
  - Database: `sonar`

---

## **Prerequisites**
1. **Docker** and **Docker Compose** installed on your machine.
   - [Install Docker](https://docs.docker.com/get-docker/)
   - [Install Docker Compose](https://docs.docker.com/compose/install/)
2. Ports **8080**, **50000**, and **9000** available on the host.

---

## **Initial Setup**
1. **Jenkins Persistence:**
   - The `jenkins_home` volume ensures that Jenkins data is not lost when the container is restarted.
2. **Docker Access for Jenkins:**
   - Binding `/var/run/docker.sock` allows Jenkins to manage Docker containers on the host.

3. **PostgreSQL Database:**
   - Preconfigured with credentials and database required by SonarQube.

---

## **How to Run**
1. Clone the repository containing this `docker-compose.yml` file or create one.
2. Navigate to the directory where the file is located.
3. Run the following command:
   ```bash
   docker-compose up -d
