📘 CEPREB – Technical Overview
(Imperatives · Should · Must · Need To — Assignment T03)
🔧 Project Stack
Component	Technology
Backend	Java 17 · Spring Boot WebFlux · Spring Data R2DBC
Database	PostgreSQL (Neon) via R2DBC
Documentation	Springdoc OpenAPI 3 (Swagger UI)
Build Tool	Maven Wrapper (mvnw.cmd)
✅ Project Purpose

CEPREB is a backend service designed to manage municipalities (tenants).
It provides:

Reactive CRUD endpoints

Validation utilities

A scalable multi-tenant configuration system

🛠️ Setup Instructions (Imperatives)

Follow these steps to run the project locally:

1️⃣ Clone the repository
git clone https://<your-repo-host>/<your-org>/cepreb.git

2️⃣ Navigate into the backend
cd back/vg-ms-tenantmanagmentservice

3️⃣ Set environment variables (PowerShell – Windows)
$env:SERVER_PORT = '5001'
$env:DB_URL = 'r2dbc:postgresql://<HOST>:5432/<DB_NAME>?sslmode=require'
$env:DB_USERNAME = '<DB_USER>'
$env:DB_PASSWORD = '<DB_PASSWORD>'

4️⃣ Run Spring Boot in dev mode
./mvnw.cmd spring-boot:run

5️⃣ Build the JAR & run it
./mvnw.cmd -DskipTests package
java -jar .\target\vg-backend-0.0.1-SNAPSHOT.jar

📝 Neon PostgreSQL Notice

You must include ?sslmode=require in your R2DBC connection URL.

$env:DB_URL = 'r2dbc:postgresql://ep-your-neon-pooler.neon.tech:5432/neondb?sslmode=require'

🧩 How to Use the API (Should)

You should access Swagger UI:
👉 http://localhost:5001/swagger-ui.html

You should begin by creating a municipality:
POST /api/municipalities

You should validate information via:

GET /api/municipalities/validate/tax-id/{taxId}
GET /api/municipalities/validate/ubigeo-code/{ubigeoCode}


You should always use UUIDs as entity identifiers.

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

You must configure these environment variables:

SERVER_PORT

DB_URL

DB_USERNAME

DB_PASSWORD

You must use a valid R2DBC PostgreSQL connection string.

You need to enable CORS for the frontend:

Environment	URL
Dev	http://localhost:5173
Prod	your final domain

You must secure actuator endpoints (/actuator/**) before deployment.

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

API Docs
/swagger-ui.html
/api-docs

🧪 Local Testing (Imperatives)
✔️ Check API Health
Invoke-WebRequest http://localhost:5001/actuator/health

✔️ List municipalities
Invoke-WebRequest http://localhost:5001/api/municipalities

✔️ Create a new municipality
Invoke-RestMethod -Method POST -Uri http://localhost:5001/api/municipalities -ContentType 'application/json' -Body '{"name":"Test","ubigeoCode":"123456","department":"DEP","province":"PROV","district":"DIST","ruc":"12345678901"}'

💡 Best Practices (Should)

You should store secrets in environment variables.

You should write WebTestClient unit tests.

You should document new endpoints in Swagger & README.

You should build before deployment:

mvn -q -DskipTests package

🧑‍🏫 Contributing Instructions (Imperatives)

Fork the repository.

Create a feature branch:

git checkout -b feature/<feature-name>


Implement and test your changes.

Submit a Pull Request with a clear explanation.

Reference an issue:

Fixes #<issue-number>

📞 Support

Open an Issue in the repository or contact the maintainers.

✔️ CEPREB – Clean, Scalable & Reactive. Ready for Production.
