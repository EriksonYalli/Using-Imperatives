<div align="center">
  <h1>CEPREB – Technical Overview</h1>
  <p><b>Backend reactivo con Spring Boot WebFlux + R2DBC (PostgreSQL)</b></p>
  <p>
    <img alt="Java 17" src="https://img.shields.io/badge/Java-17-007396?logo=java&logoColor=white">
    <img alt="Spring Boot" src="https://img.shields.io/badge/Spring%20Boot-3.1.5-6DB33F?logo=springboot&logoColor=white">
    <img alt="WebFlux" src="https://img.shields.io/badge/WebFlux-reactive-6DB33F">
    <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-R2DBC-336791?logo=postgresql&logoColor=white">
    <img alt="Maven" src="https://img.shields.io/badge/Maven-wrapper-C71A36?logo=apachemaven&logoColor=white">
    <img alt="Docker" src="https://img.shields.io/badge/Docker-ready-2496ED?logo=docker&logoColor=white">
  </p>
  <p>
    <a href="#project-stack">Stack</a> ·
    <a href="#project-purpose">Purpose</a> ·
    <a href="#setup-instructions-imperatives">Setup</a> ·
    <a href="#how-to-use-the-app-advice-with-should">Uso</a> ·
    <a href="#future-plans-advice--suggestions">Roadmap</a> ·
    <a href="#repository-structure">Estructura</a>
  </p>
</div>

---

## Tabla de Contenidos

- **[Project Stack](#project-stack)**
- **[Project Purpose](#project-purpose)**
- **[Setup Instructions (Imperatives)](#setup-instructions-imperatives)**
- **[How to Use the App (Advice with “should”)](#how-to-use-the-app-advice-with-should)**
- **[Future Plans (Advice & Suggestions)](#future-plans-advice--suggestions)**
- **[Repository Structure](#repository-structure)**
- **[Contributing (Imperatives & Advice)](#contributing-imperatives--advice)**
- **[Deployment Requirements (Must & Need To)](#deployment-requirements-must--need-to)**
- **[Best Practices & Tips](#best-practices--tips)**
- **[Questions & Support](#questions--support)**
- **[Notas de seguridad](#notas-de-seguridad)**

---

## Project Stack

- **Backend**: Java 17, Spring Boot 3.1.5
- **Reactive**: Spring WebFlux
- **Data**: Spring Data R2DBC
- **Database**: PostgreSQL (Neon) vía R2DBC
- **Build**: Maven Wrapper
- **Containers**: Docker + Docker Compose

---

## Project Purpose

API reactiva que expone endpoints y persiste datos en PostgreSQL utilizando R2DBC (no bloqueante), ideal para servicios de alto rendimiento y operaciones I/O intensivas.

---

## Setup Instructions (Imperatives)

- **Clonar el repositorio**:
  - `git clone https://github.com/YourOrg/cepreb.git`
- **Entrar al backend**:
  - `cd cepreb/Using-Imperatives`
- **Construir (PowerShell)**:
  - `./mvnw.cmd clean package`
- **Configurar variables de entorno (PowerShell)**:
  - `$env:SPRING_R2DBC_URL = 'r2dbc:postgresql://<USER>:<PASS>@<HOST>:5432/<DB>?sslMode=VERIFY_FULL'`
  - `$env:SPRING_R2DBC_USERNAME = '<USER>'`
  - `$env:SPRING_R2DBC_PASSWORD = '<PASS>'`
  - `$env:SERVER_PORT = '5001'`  (por defecto 5001)
- **Ejecutar la app**:
  - `./mvnw.cmd spring-boot:run`
- **Levantar con Docker Compose**:
  - `docker compose up --build`
  - El compose mapea por defecto `5003:5003` (ajústalo si es necesario).

> Importante: evita credenciales hardcodeadas en `application.yml` y `docker-compose.yml`. Usa variables de entorno o un gestor de secretos.

---

## How to Use the App (Advice with “should”)

- You should abrir `http://localhost:5001` al correr local con `SERVER_PORT=5001`.
- You should usar `http://localhost:5003` si levantas con Docker Compose.
- You should habilitar CORS si tu frontend va a consumir el API.

### Endpoints de ejemplo

| Método | Ruta             | Descripción                             |
|--------|------------------|-----------------------------------------|
| GET    | `/api/hello`     | Endpoint de prueba/estado del servicio. |
| POST   | `/api/people`    | Crea un recurso Person (JSON body).     |

> Tip: Usa `curl`, Postman o Thunder Client para validar rápidamente el contrato de los endpoints.

---

## Future Plans (Advice & Suggestions)

- We should parametrizar completamente `spring.r2dbc.url` y usar perfiles (`application-dev.yml`, `application-prod.yml`).
- We should añadir migraciones de base de datos con Flyway/Liquibase (R2DBC compatible).
- We should integrar observabilidad (Spring Boot Actuator, Prometheus, logs estructurados).
- We should incrementar test coverage (WebFlux, servicios y repositorios R2DBC).
- We should asegurar SSL con Neon y rotación de secretos (.env local + secret manager en despliegue).
- We should documentar el contrato de `POST /api/people` (payload, validaciones, respuestas) con OpenAPI/Swagger.

---

## Repository Structure

- **/Using-Imperatives**
  - `pom.xml` (Spring Boot 3.1.5, Java 17, WebFlux, R2DBC, Lombok)
  - `Dockerfile` (multi-stage build con Maven 3.9.6 y Temurin 17)
  - `docker-compose.yml` (servicio `vg-backend`, variables `SPRING_R2DBC_*`, puerto 5003)
  - `src/main/java/pe/edu/vallegrande/configurationservice/configurationservice.java` (clase main)
  - `src/main/resources/application.yml` (server.port 5001; config R2DBC)
  - `README.md` (este documento)

---

## Contributing (Imperatives & Advice)

- Fork del repo.
- Crear una rama de feature:
  - `git checkout -b feature/tu-feature`
- Implementar, probar y lint localmente.
- Abrir un Pull Request con resumen y descripción claros.
- You should añadir “Fixes #<issue-number>” si está relacionado a un issue.

---

## Deployment Requirements (Must & Need To)

- You must definir variables de entorno seguras (no hardcode):
  - `SPRING_R2DBC_URL`
  - `SPRING_R2DBC_USERNAME`
  - `SPRING_R2DBC_PASSWORD`
  - `SERVER_PORT`
- You need to habilitar CORS en la configuración de Spring para el dominio del frontend.
- You must usar perfiles y secretos seguros en producción (no commitear `.env`).
- You must construir la imagen o usar Compose para desplegar:
  - `docker build -t cepreb-backend .`
  - `docker compose up --build`

---

## Best Practices & Tips

- You should escribir tests para WebFlux, servicios y repositorios R2DBC.
- You should documentar endpoints y modelos con OpenAPI/Swagger.
- You should usar `./mvnw.cmd clean` antes de empaquetar.
- You should extraer valores sensibles a variables de entorno o un vault.

---

## Questions & Support

- Abrir un issue en este repositorio.
- Etiquetar a los líderes del proyecto para temas urgentes.
- Unirse al canal de chat del equipo para colaboración en tiempo real.

---

### Notas de seguridad

- Si existen credenciales en archivos de configuración, muévelas a variables de entorno cuanto antes.
