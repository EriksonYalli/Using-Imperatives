CEPREB – Technical Overview

(Imperatives, Should, Must, Need To – Assignment T03)

🔧 Project Stack

Backend: Java 17 (Spring Boot WebFlux, Spring Data R2DBC)

Database: PostgreSQL (Neon) via R2DBC

Documentation: Springdoc OpenAPI 3 (Swagger UI)

Build Tool: Maven Wrapper (mvnw.cmd)

✅ Project Purpose

CEPREB is a backend service designed to manage municipalities (tenants). It provides reactive CRUD endpoints, validation tools, and scalable configuration features to support multi-tenant municipal platforms.

🛠️ Setup Instructions (Imperatives)

Follow these steps to run the project locally:

1. Clone the repository
git clone https://<your-repo-host>/<your-org>/<cepreb>.git

2. Navigate into the backend service
cd back/vg-ms-tenantmanagmentservice

3. Set environment variables (PowerShell – Windows)
$env:SERVER_PORT = '5001'
$env:DB_URL = 'r2dbc:postgresql://<HOST>:5432/<DB_NAME>?sslmode=require'
$env:DB_USERNAME = '<DB_USER>'
$env:DB_PASSWORD = '<DB_PASSWORD>'

4. Run Spring Boot (development mode)
./mvnw.cmd spring-boot:run

5. Alternatively, build the JAR and run it
./mvnw.cmd -DskipTests package
java -jar .\target\vg-backend-0.0.1-SNAPSHOT.jar

Neon PostgreSQL Note

You must include ?sslmode=require in the R2DBC URL.
Example:

$env:DB_URL = 'r2dbc:postgresql://ep-your-neon-pooler.neon.tech:5432/neondb?sslmode=require'

🧩 How to Use the API (Should)

You should access Swagger UI here:
👉 http://localhost:5001/swagger-ui.html

You should start by creating a municipality using:
POST /api/municipalities

You should validate data using:

/api/municipalities/validate/tax-id/{taxId}

/api/municipalities/validate/ubigeo-code/{ubigeoCode}

You should always use UUIDs for IDs to maintain consistency.

You should review 4xx/5xx responses to check validation details.

📁 Repository Structure
/back
└── vg-ms-tenantmanagmentservice
    ├── src
    │   ├── main
    │   │   ├── java/pe/edu/vallegrande/configurationservice
    │   │   │   ├── configurationservice.java
    │   │   │   ├── controller/MunicipalityController.java
    │   │   │   ├── model/Municipality.java
    │   │   │   ├── repository/MunicipalityRepository.java
    │   │   │   └── service/... (impl/MunicipalityServiceImpl.java)
    │   │   └── resources
    │   │       ├── application.yml
    │   │       └── schema.sql
    │   └── test
    ├── pom.xml
    ├── README.md
    └── README-IMPERATIVES.md

🚀 Deployment Requirements (Must & Need To)

You must configure these environment variables in any environment:

SERVER_PORT

DB_URL

DB_USERNAME

DB_PASSWORD

You must use a valid R2DBC PostgreSQL connection string.

You need to enable CORS with your frontend domain:

Dev: http://localhost:5173

Prod: your real domain

You must secure actuator endpoints before deployment.

🔗 Key API Endpoints
CRUD

GET /api/municipalities

GET /api/municipalities/{id}

POST /api/municipalities

PUT /api/municipalities/{id}

PATCH /api/municipalities/{id}

DELETE /api/municipalities/{id}

Validation

GET /api/municipalities/validate/tax-id/{taxId}

GET /api/municipalities/validate/ubigeo-code/{ubigeoCode}

API Docs

/swagger-ui.html

/api-docs

🧪 Local Testing (Imperatives)
1. Check health
Invoke-WebRequest http://localhost:5001/actuator/health

2. List municipality records
Invoke-WebRequest http://localhost:5001/api/municipalities

3. Create a new municipality
Invoke-RestMethod -Method POST -Uri http://localhost:5001/api/municipalities -ContentType 'application/json' -Body '{"name":"Test","ubigeoCode":"123456","department":"DEP","province":"PROV","district":"DIST","ruc":"12345678901"}'

💡 Best Practices (Should)

You should store secrets in environment variables, not Git.

You should add unit tests with WebTestClient for controllers.

You should document any new endpoints in Swagger or this README.

You should run:

mvn -q -DskipTests package


before deployment.

🧑‍🏫 Contributing (Imperatives)

Fork the repository.

Create a feature branch:

git checkout -b feature/<feature-name>


Implement and test your changes.

Submit a Pull Request with a clear explanation.

Reference issues:

Fixes #<issue-number>

📞 Support

Open an issue in the repository or contact the maintainers.

✔️ CEPREB – Clean, Scalable & Reactive. Ready for Production.
