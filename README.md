<div align="center">
  <img alt="cepreb – Technical Overview" src="https://capsule-render.vercel.app/api?type=rounded&color=gradient&height=160&text=cepreb%20%E2%80%93%20Technical%20Overview&fontSize=56&fontAlign=50&fontAlignY=50&fontColor=ffffff" />
  <h3>Service: vg-ms-tenantmanagmentservice</h3>
  <p><b>Reactive backend with Spring Boot WebFlux + R2DBC (PostgreSQL)</b></p>
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
    <a href="#how-to-use-the-app-advice-with-should">Usage</a> ·
    <a href="#future-plans-advice--suggestions">Roadmap</a> ·
    <a href="#repository-structure">Structure</a>
  </p>
</div>

---

## Table of Contents

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
- **[Security Notes](#security-notes)**

---

## 🔧 Project Stack

- **Backend**: Java 17, Spring Boot 3.1.5
- **Reactive**: Spring WebFlux
- **Data**: Spring Data R2DBC
- **Database**: PostgreSQL (Neon) via R2DBC
- **Build**: Maven Wrapper
- **Containers**: Docker + Docker Compose

---

## ✅ Project Purpose

Reactive API that exposes endpoints and persists data in PostgreSQL using R2DBC (non‑blocking). It fits high‑throughput, I/O‑intensive services.

---

## 🛠️ Setup Instructions (Imperatives)

- **Clone the repository**:
  - `git clone https://github.com/YourOrg/cepreb.git`
- **Go to the backend**:
  - `cd cepreb/Using-Imperatives`
- **Build (PowerShell)**:
  - `./mvnw.cmd clean package`
- **Set environment variables (PowerShell)**:
  - `$env:SPRING_R2DBC_URL = 'r2dbc:postgresql://<USER>:<PASS>@<HOST>:5432/<DB>?sslMode=VERIFY_FULL'`
  - `$env:SPRING_R2DBC_USERNAME = '<USER>'`
  - `$env:SPRING_R2DBC_PASSWORD = '<PASS>'`
  - `$env:SERVER_PORT = '5001'`  (default 5001)
- **Run the app**:
  - `./mvnw.cmd spring-boot:run`
- **Run with Docker Compose**:
  - `docker compose up --build`
  - Default port mapping is `5003:5003` (adjust as needed).

> Important: avoid hardcoded credentials in `application.yml` and `docker-compose.yml`. Prefer environment variables or a secrets manager.

---

## 🧩 How to Use the App (Advice with “should”)

- You should open `http://localhost:5001` when running locally with `SERVER_PORT=5001`.
- You should use `http://localhost:5003` when running via Docker Compose.
- You should enable CORS if a frontend will consume the API.

### 📚 Sample Endpoints

| Method | Path                                            | Description                                              |
|--------|--------------------------------------------------|----------------------------------------------------------|
| GET    | `/api/municipalities`                           | List all municipalities.                                 |
| GET    | `/api/municipalities/{id}`                      | Get municipality by ID (UUID).                           |
| POST   | `/api/municipalities`                           | Create municipality.                                     |
| PATCH  | `/api/municipalities/{id}`                      | Partially update municipality by ID.                     |
| PUT    | `/api/municipalities/{id}`                      | Replace municipality by ID.                              |
| DELETE | `/api/municipalities/{id}`                      | Delete municipality by ID.                               |
| GET    | `/api/municipalities/validate/tax-id/{taxId}`   | Validate tax ID (RUC). Optional: `?excludeId=<UUID>`.    |
| GET    | `/api/municipalities/validate/ubigeo-code/{ub}` | Validate ubigeo code. Optional: `?excludeId=<UUID>`.     |

> Tip: Use `curl`, Postman, or Thunder Client to quickly validate endpoint contracts.

---

## 🎯 Future Plans (Advice & Suggestions)

- We should fully parameterize `spring.r2dbc.url` and use profiles (`application-dev.yml`, `application-prod.yml`).
- We should add database migrations with Flyway/Liquibase (R2DBC compatible).
- We should integrate observability (Spring Boot Actuator, Prometheus, structured logs).
- We should increase test coverage (WebFlux, services, and R2DBC repositories).
- We should enforce SSL with Neon and rotate secrets (.env locally, secrets manager in prod).
- We should document the `POST /api/people` contract (payload, validation, responses) with OpenAPI/Swagger.

---

## 📁 Repository Structure

```text
/cepreb
├── Using-Imperatives/          # Spring Boot WebFlux + R2DBC backend (service: vg-ms-tenantmanagmentservice)
│   ├── pom.xml                 # Dependencies and config (Java 17, Spring Boot 3.1.5)
│   ├── Dockerfile              # Multi-stage container build
│   ├── docker-compose.yml      # Backend service and SPRING_R2DBC_* variables
│   ├── src/
│   │   ├── main/java/pe/edu/vallegrande/configurationservice/
│   │   │   └── configurationservice.java   # Main class
│   │   └── main/resources/application.yml  # server.port and R2DBC config
│   └── README.md               # ← You are here
├── docs/                       # Project documentation & diagrams (optional)
└── .env.example                # Environment variables template (optional)
```

---

## 🧑‍🏫 Contributing (Imperatives & Advice)

- Fork this repository.
- Create a feature branch:
  - `git checkout -b feature/your-feature`
- Implement, test, and lint locally.
- Open a Pull Request with a clear summary and description.
- You should add “Fixes #<issue-number>” if it relates to an open issue.

---

## 🚀 Deployment Requirements (Must & Need To)

- You must set secure environment variables (no hardcoding):
  - `SPRING_R2DBC_URL`
  - `SPRING_R2DBC_USERNAME`
  - `SPRING_R2DBC_PASSWORD`
  - `SERVER_PORT`
- You need to enable CORS in Spring config for the frontend domain.
- You must use profiles and secure secrets in production (do not commit `.env`).
- You must build the image or use Compose to deploy:
  - `docker build -t cepreb-backend .`
  - `docker compose up --build`

---

## 💡 Best Practices & Tips

- You should write tests for WebFlux, services, and R2DBC repositories.
- You should document endpoints and models with OpenAPI/Swagger.
- You should run `./mvnw.cmd clean` before packaging.
- You should move sensitive values to environment variables or a secrets vault.

---

## 📞 Questions & Support

- Open an issue in this repository.
- Tag the project leads for urgent matters.
- Join the team chat for real-time collaboration.

---

### 🔒 Security Notes

- If any credentials exist in config files, move them to environment variables ASAP.
