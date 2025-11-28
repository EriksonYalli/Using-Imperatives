📘 CEPREB – Technical Overview
Imperatives · Should · Must · Need To — Assignment T03
🔧 Project Stack

Backend: Java 17 · Spring Boot WebFlux · Spring Data R2DBC
Database: PostgreSQL (Neon, vía R2DBC)
Documentation: Springdoc OpenAPI 3 (Swagger UI)
Build Tool: Maven Wrapper (mvnw.cmd)

✅ Project Purpose

CEPREB is a backend service designed to manage municipalities (tenants).
It provides:

Reactive CRUD endpoints

Validation utilities

A scalable multi-tenant configuration system

🛠️ Setup Instructions (Imperatives)
1. Clone the repository
git clone https://cepreb.git

2. Navigate into the backend
cd back/vg-ms-tenantmanagmentservice

3. Set environment variables (PowerShell – Windows)
$env:SERVER_PORT = '5001'
$env:DB_URL = 'r2dbc:postgresql://<HOST>:5432/<DB_NAME>?sslmode=require'
$env:DB_USERNAME = '<DB_USER>'
$env:DB_PASSWORD = '<DB_PASSWORD>'

4. Run Spring Boot
./mvnw.cmd spring-boot:run

5. Build JAR
./mvnw.cmd -DskipTests package
java -jar .\target\vg-backend-0.0.1-SNAPSHOT.jar

📝 Neon PostgreSQL (Required)

Use SSL:

?sslmode=require


Example:

$env:DB_URL = 'r2dbc:postgresql://ep-neon-pooler.neon.tech:5432/neondb?sslmode=require'

📁 Repository Structure
/back
└── vg-ms-tenantmanagmentservice
    ├── src/main/java/...
    ├── resources/application.yml
    ├── schema.sql
    ├── pom.xml
    ├── README.md

🔗 Key API Endpoints
CRUD
GET    /api/municipalities
GET    /api/municipalities/{id}
POST   /api/municipalities
PUT    /api/municipalities/{id}
PATCH  /api/municipalities/{id}
DELETE /api/municipalities/{id}

Validation
GET /api/municipalities/validate/tax-id/{taxId}
GET /api/municipalities/validate/ubigeo-code/{ubigeoCode}

Swagger
/swagger-ui.html
/api-docs

🧪 Local Testing

Check API health:

Invoke-WebRequest http://localhost:5001/actuator/health


List municipalities:

Invoke-WebRequest http://localhost:5001/api/municipalities

✔️ Best Practices

Use environment variables for secrets

Create WebTestClient unit tests

Document new endpoints
