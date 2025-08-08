# Development Environment Setup

This guide provides step-by-step instructions for setting up your development environment for the E-Commerce Microservices project.

## Prerequisites

### Required Software

#### 1. Java Development Kit (JDK)
- **Version**: Java [JAVA_VERSION] or later
- **Download**: [Oracle JDK](https://www.oracle.com/java/technologies/downloads/) or [OpenJDK](https://adoptium.net/)
- **Installation**: Follow platform-specific installation instructions
- **Verification**: `java -version` should show Java [JAVA_VERSION]+

#### 2. Apache Maven
- **Version**: [MAVEN_VERSION] or later
- **Download**: [Maven Official Site](https://maven.apache.org/download.cgi)
- **Installation**: Extract to a directory and add to PATH
- **Verification**: `mvn -version` should show Maven [MAVEN_VERSION]+

#### 3. Docker Desktop
- **Download**: [Docker Desktop](https://www.docker.com/products/docker-desktop)
- **Installation**: Follow platform-specific installation instructions
- **Requirements**: 
  - Windows: WSL2 enabled
  - macOS: No additional requirements
  - Linux: Docker Engine
- **Verification**: `docker --version` and `docker-compose --version`

#### 4. Git
- **Download**: [Git Official Site](https://git-scm.com/downloads)
- **Installation**: Follow platform-specific installation instructions
- **Verification**: `git --version`

### Optional but Recommended

#### 5. IDE (Choose One)
- **IntelliJ IDEA**: [Community Edition](https://www.jetbrains.com/idea/download/) (Free) or Ultimate Edition
- **VS Code**: [Download](https://code.visualstudio.com/) with Java extensions
- **Eclipse**: [Download](https://www.eclipse.org/downloads/) with Spring Tools

#### 6. Database Management Tools
- **pgAdmin**: [Download](https://www.pgadmin.org/download/) for PostgreSQL
- **MongoDB Compass**: [Download](https://www.mongodb.com/try/download/compass) for MongoDB
- **RedisInsight**: [Download](https://redis.com/redis-enterprise/redis-insight/) for Redis

#### 7. API Testing Tools
- **Postman**: [Download](https://www.postman.com/downloads/)
- **Insomnia**: [Download](https://insomnia.rest/download)

## Environment Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd microservices-app
```

### 2. Verify Prerequisites
```bash
# Check Java version
java -version

# Check Maven version
mvn -version

# Check Docker
docker --version
docker-compose --version

# Check Git
git --version
```

### 3. IDE Configuration

#### IntelliJ IDEA Setup
1. **Import Project**: File → Open → Select project root
2. **Maven Import**: Import Maven projects automatically
3. **Java Version**: Set project SDK to Java [JAVA_VERSION]
4. **Lombok**: Install Lombok plugin if using Lombok
5. **Docker**: Install Docker plugin for container management

#### VS Code Setup
1. **Java Extension Pack**: Install Java Extension Pack
2. **Spring Boot Extension**: Install Spring Boot Extension Pack
3. **Docker Extension**: Install Docker extension
4. **Maven Extension**: Install Maven for Java extension

### 4. Docker Configuration

#### Enable Docker Compose
```bash
# Verify Docker Compose is available
docker-compose --version

# If not available, install separately
# Windows/macOS: Included with Docker Desktop
# Linux: sudo apt-get install docker-compose
```

#### Docker Resources (Windows/macOS)
1. Open Docker Desktop
2. Go to Settings → Resources
3. Allocate sufficient resources:
   - **Memory**: 8GB minimum, 16GB recommended
   - **CPU**: 4 cores minimum, 8 cores recommended
   - **Disk**: 50GB minimum

### 5. Local Development Environment

#### Start Infrastructure Services
```bash
# Navigate to infrastructure directory
cd infrastructure/docker-compose

# Start all services
docker-compose up -d

# Verify services are running
docker-compose ps
```

#### Services Started:
- **PostgreSQL**: Port 5432
- **MongoDB**: Port 27017
- **Redis**: Port 6379
- **Elasticsearch**: Port 9200
- **Kafka**: Port 9092
- **RabbitMQ**: Port 5672
- **Keycloak**: Port 8080
- **Prometheus**: Port 9090
- **Grafana**: Port 3000
- **Jaeger**: Port 16686

### 6. Database Setup

#### PostgreSQL Setup
```bash
# Connect to PostgreSQL
docker exec -it postgres psql -U postgres

# Create databases (if not auto-created)
CREATE DATABASE user_service;
CREATE DATABASE order_service;
CREATE DATABASE payment_service;
CREATE DATABASE analytics_service;
```

#### MongoDB Setup
```bash
# Connect to MongoDB
docker exec -it mongodb mongosh

# Create databases (auto-created on first use)
use inventory_service
use notification_service
```

#### Redis Setup
```bash
# Connect to Redis
docker exec -it redis redis-cli

# Test connection
ping
```

### 7. Keycloak Setup

#### Access Keycloak Admin Console
1. Open browser: `http://localhost:8080`
2. Login: `admin` / `admin`
3. Create realm: `ecommerce`
4. Create clients for each service
5. Create users and roles

#### Keycloak Configuration
```bash
# Import realm configuration (if available)
# Use Keycloak admin console or REST API
```

### 8. Environment Variables

#### Create Environment Files
```bash
# Create .env file in project root
cp .env.example .env

# Edit .env file with your configuration
nano .env
```

#### Required Environment Variables
```bash
# Database URLs
POSTGRES_URL=jdbc:postgresql://localhost:5432/
MONGODB_URL=mongodb://localhost:27017/
REDIS_URL=redis://localhost:6379

# Keycloak Configuration
KEYCLOAK_URL=http://localhost:8080
KEYCLOAK_REALM=ecommerce
KEYCLOAK_CLIENT_ID=api-gateway

# Kafka Configuration
KAFKA_BOOTSTRAP_SERVERS=localhost:9092

# RabbitMQ Configuration
RABBITMQ_URL=amqp://localhost:5672
```

### 9. Build and Test

#### Build All Services
```bash
# Build all services
mvn clean install -DskipTests

# Build with tests
mvn clean install
```

#### Run Integration Tests
```bash
# Run integration tests
mvn test -Dtest=*IntegrationTest

# Run with Testcontainers
mvn test -Dspring.profiles.active=test
```

### 10. Start Services

#### Development Mode
```bash
# Start API Gateway
cd api-gateway
mvn spring-boot:run

# Start User Service
cd ../user-service
mvn spring-boot:run

# Start other services similarly
```

#### Using IDE
1. Open each service project in IDE
2. Run main application class
3. Configure VM options if needed

### 11. Database Migration Tools

#### Flyway (PostgreSQL)
- Used for managing and applying schema migrations for all PostgreSQL databases.
- Migration scripts are located in each service's `src/main/resources/db/migration` directory.
- Migrations are applied automatically on service startup if Flyway is enabled in the configuration.
- For manual migration, use:
  ```bash
  mvn flyway:migrate -Dflyway.configFiles=src/main/resources/flyway.conf
  ```
- See service-specific README or configuration for details.

#### Mongock (MongoDB)
- Used for managing schema changes and data migrations for MongoDB-based services.
- Migration scripts are located in each service's `src/main/resources/mongock` directory.
- Migrations are applied automatically on service startup if Mongock is enabled in the configuration.
- See service-specific README or configuration for details.

## Troubleshooting

### Common Issues

#### Docker Issues
```bash
# Check Docker status
docker info

# Restart Docker Desktop
# Windows/macOS: Restart Docker Desktop application
# Linux: sudo systemctl restart docker
```

#### Port Conflicts
```bash
# Check if ports are in use
netstat -tulpn | grep :8080
netstat -tulpn | grep :5432

# Stop conflicting services or change ports in docker-compose.yml
```

#### Memory Issues
```bash
# Check available memory
free -h

# Increase Docker memory allocation
# Windows/macOS: Docker Desktop Settings → Resources → Memory
```

#### Database Connection Issues
```bash
# Check if databases are running
docker-compose ps

# Check database logs
docker-compose logs postgres
docker-compose logs mongodb
```

## Next Steps

After completing the setup:

1. **Review Architecture**: Read the [Architecture Decision Records](../architecture/adr/)
2. **Start Development**: Follow the [Service Startup Guide](service-startup.md)
3. **API Documentation**: Access Swagger UI at `http://localhost:8080/swagger-ui.html`
4. **Monitoring**: Access Grafana at `http://localhost:3000` (admin/admin)
5. **Tracing**: Access Jaeger at `http://localhost:16686`
