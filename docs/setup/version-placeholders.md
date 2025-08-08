# Version Placeholders

This document lists all the version placeholders used throughout the project documentation that need to be replaced with actual version numbers.

## Framework Versions

### Java and Build Tools
- `[JAVA_VERSION]` - Java version (e.g., 17, 21)
- `[MAVEN_VERSION]` - Apache Maven version (e.g., 3.8.0, 3.9.0)
- `[SPRING_BOOT_VERSION]` - Spring Boot version (e.g., 3.2.0, 3.3.0)

### Database Versions
- `[POSTGRESQL_VERSION]` - PostgreSQL version (e.g., 15, 16)
- `[MONGODB_VERSION]` - MongoDB version (e.g., 6.0, 7.0)
- `[REDIS_VERSION]` - Redis version (e.g., 7.0, 7.2)
- `[ELASTICSEARCH_VERSION]` - Elasticsearch version (e.g., 8.0, 8.11)

### Message Queue Versions
- `[KAFKA_VERSION]` - Apache Kafka version (e.g., 3.4, 3.6)
- `[RABBITMQ_VERSION]` - RabbitMQ version (e.g., 3.11, 3.12)

### Authentication and Security
- `[KEYCLOAK_VERSION]` - Keycloak version (e.g., 22.0, 23.0)

### Monitoring and Observability
- `[PROMETHEUS_VERSION]` - Prometheus version (e.g., 2.45, 2.47)
- `[GRAFANA_VERSION]` - Grafana version (e.g., 10.0, 10.2)
- `[JAEGER_VERSION]` - Jaeger version (e.g., 1.48, 1.50)

### Testing Tools
- `[TESTCONTAINERS_VERSION]` - Testcontainers version (e.g., 1.18, 1.19)
- `[JUNIT_VERSION]` - JUnit version (e.g., 5.9, 5.10)

### Container and Orchestration
- `[DOCKER_VERSION]` - Docker version (e.g., 24.0, 25.0)
- `[KUBERNETES_VERSION]` - Kubernetes version (e.g., 1.28, 1.29)

## How to Update Placeholders

1. **Search and Replace**: Use your IDE's search and replace functionality to find all instances of these placeholders
2. **Documentation Files**: Update placeholders in all `.md` files in the `docs/` directory
3. **Configuration Files**: Update placeholders in configuration files like `pom.xml`, `docker-compose.yml`, etc.
4. **README Files**: Update placeholders in the main README and service-specific README files

## Example Search Patterns

```bash
# Find all placeholder instances
grep -r "\[.*_VERSION\]" docs/
grep -r "\[.*_VERSION\]" . --include="*.md"
grep -r "\[.*_VERSION\]" . --include="*.yml"
grep -r "\[.*_VERSION\]" . --include="*.xml"
```

## Recommended Versions (Latest Stable)

As of the last update, here are the recommended stable versions:

- **Java**: 21 (LTS)
- **Spring Boot**: 3.2.0
- **PostgreSQL**: 16
- **MongoDB**: 7.0
- **Redis**: 7.2
- **Elasticsearch**: 8.11
- **Kafka**: 3.6
- **RabbitMQ**: 3.12
- **Keycloak**: 23.0
- **Prometheus**: 2.47
- **Grafana**: 10.2
- **Jaeger**: 1.50
- **Testcontainers**: 1.19
- **JUnit**: 5.10
- **Docker**: 25.0
- **Kubernetes**: 1.29

## Version Compatibility Matrix

When updating versions, ensure compatibility between:

1. **Spring Boot and Java**: Spring Boot 3.x requires Java 17+
2. **Spring Boot and Spring Cloud**: Use compatible versions
3. **Database Drivers**: Ensure database driver versions match database versions
4. **Testcontainers**: Ensure Testcontainers supports the database versions you're using

## Notes

- Always test the application after updating versions
- Check for breaking changes in major version updates
- Update Docker images in `docker-compose.yml` to match new versions
- Update Maven dependencies in `pom.xml` files
- Update Kubernetes manifests if using specific image tags
