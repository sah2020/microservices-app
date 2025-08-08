# E-Commerce Microservices Portfolio Project

A comprehensive microservices architecture showcasing modern Java technologies, patterns, and best practices for portfolio demonstration.

## 🏗️ Architecture Overview

This project demonstrates a complete e-commerce microservices ecosystem with the following services:

- **API Gateway** - Single entry point with routing and security
- **User Management Service** - Authentication, authorization, and user profiles
- **Order Management Service** - Order lifecycle with event sourcing and CQRS
- **Inventory Management Service** - Stock management and product catalog
- **Payment Processing Service** - Mock payment processing with SAGA patterns
- **Notification Service** - Event-driven notifications using Kafka
- **Analytics Service** - Business intelligence and reporting

## �� Quick Start

1. **Prerequisites**: Follow [Development Environment Setup](./docs/setup/development-environment.md)
2. **Local Development**: Run `docker-compose up` in the `infrastructure/docker-compose` directory
3. **Start Services**: Follow [Service Startup Guide](./docs/setup/service-startup.md)
4. **API Documentation**: Access Swagger UI at `http://localhost:8080/swagger-ui.html`

## �� Documentation

- [Architecture Decision Records](./docs/architecture/adr/) - Technical decisions and rationale
- [Development Setup](./docs/setup/) - Environment and tool configuration

## 🛠️ Technology Stack

### Core Framework
- **Spring Boot [SPRING_BOOT_VERSION]** - Application framework
- **Spring Cloud** - Microservices patterns
- **Java [JAVA_VERSION]** - Programming language

### Data Storage
- **PostgreSQL [POSTGRESQL_VERSION]** - Relational data (User, Order, Payment, Analytics)
- **MongoDB [MONGODB_VERSION]** - Document storage (Inventory, Notifications)
- **Redis [REDIS_VERSION]** - Caching and sessions
- **Elasticsearch [ELASTICSEARCH_VERSION]** - Search and analytics

### Messaging & Events
- **Apache Kafka [KAFKA_VERSION]** - Event streaming and notifications
- **RabbitMQ [RABBITMQ_VERSION]** - Message queuing for payments
- **Spring Cloud Stream** - Event processing

### Security & Authentication
- **Keycloak [KEYCLOAK_VERSION]** - OAuth2/OpenID Connect provider
- **Spring Security** - Application security
- **JWT** - Token-based authentication

### Observability
- **Prometheus [PROMETHEUS_VERSION]** - Metrics collection
- **Grafana [GRAFANA_VERSION]** - Visualization and dashboards
- **Jaeger [JAEGER_VERSION]** - Distributed tracing

### Testing
- **Testcontainers [TESTCONTAINERS_VERSION]** - Integration testing
- **WireMock** - API mocking
- **ArchUnit** - Architecture testing

## 📁 Project Structure

```
microservices-app/
├── 🚪 api-gateway/                    # Spring Cloud Gateway - Single entry point
│   ├── src/main/java/
│   ├── src/main/resources/
│   └── pom.xml
│
├── 👤 user-service/                   # User Management & Authentication
│   ├── src/main/java/
│   │   ├── controller/               # REST controllers
│   │   ├── service/                  # Business logic
│   │   ├── repository/               # Data access layer
│   │   ├── model/                    # Domain entities
│   │   └── config/                   # Configuration classes
│   ├── src/main/resources/
│   └── pom.xml
│
├── 📦 order-service/                  # Order Processing with CQRS & Event Sourcing
│   ├── src/main/java/
│   │   ├── command/                  # Command handlers
│   │   ├── query/                    # Query handlers
│   │   ├── event/                    # Domain events
│   │   ├── aggregate/                # Domain aggregates
│   │   └── config/
│   ├── src/main/resources/
│   └── pom.xml
│
├── 📚 inventory-service/              # Inventory & Catalog Management
│   ├── src/main/java/
│   │   ├── controller/
│   │   ├── service/
│   │   ├── repository/
│   │   ├── model/
│   │   └── config/
│   ├── src/main/resources/
│   └── pom.xml
│
├── 💳 payment-service/                # Payment Processing with SAGA Pattern
│   ├── src/main/java/
│   │   ├── controller/
│   │   ├── service/
│   │   ├── saga/                     # SAGA orchestration
│   │   ├── model/
│   │   └── config/
│   ├── src/main/resources/
│   └── pom.xml
│
├── 🔔 notification-service/           # Event-Driven Notifications
│   ├── src/main/java/
│   │   ├── listener/                 # Event listeners
│   │   ├── service/
│   │   ├── template/                 # Notification templates
│   │   └── config/
│   ├── src/main/resources/
│   └── pom.xml
│
├── 📊 analytics-service/              # Business Intelligence & Reporting
│   ├── src/main/java/
│   │   ├── controller/
│   │   ├── service/
│   │   ├── repository/
│   │   ├── model/
│   │   └── config/
│   ├── src/main/resources/
│   └── pom.xml
│
├── 📚 shared-libraries/               # Common DTOs, Utilities & Contracts
│   ├── common-dto/                   # Shared data transfer objects
│   ├── common-utils/                 # Utility classes
│   ├── event-contracts/              # Event schemas
│   └── pom.xml
│
├── 🏗️ infrastructure/                 # DevOps & Infrastructure
│   ├── docker-compose/               # Local development setup
│   ├── kubernetes/                   # K8s manifests
│   ├── monitoring/                   # Prometheus & Grafana configs
│   ├── database/                     # Database scripts
│   └── nginx/                        # Reverse proxy config
│
├── 📖 docs/                          # Project Documentation
│   ├── architecture/                 # Architecture decisions
│   │   └── adr/                      # Architecture Decision Records
│   ├── api/                          # API documentation
│   ├── setup/                        # Setup guides
│   └── deployment/                   # Deployment guides
│
└── 🔧 scripts/                       # Build & Deployment Scripts
    ├── build/                        # Build automation
    ├── deploy/                       # Deployment scripts
    └── test/                         # Test automation
```

### 🎯 Service Responsibilities

| Service | Port | Database | Key Features |
|---------|------|----------|--------------|
| **API Gateway** | 8080 | - | Routing, Security, Rate Limiting |
| **User Service** | 8081 | PostgreSQL | Auth, User Management, Profiles |
| **Order Service** | 8082 | PostgreSQL | CQRS, Event Sourcing, SAGA |
| **Inventory Service** | 8083 | MongoDB | Stock Management, Catalog |
| **Payment Service** | 8084 | PostgreSQL | Payment Processing, SAGA |
| **Notification Service** | 8085 | MongoDB | Event-driven Notifications |
| **Analytics Service** | 8086 | PostgreSQL | BI, Reporting, Dashboards |
