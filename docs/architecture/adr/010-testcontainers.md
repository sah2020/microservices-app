# ADR-010: Testcontainers for Integration Testing

## Status
Accepted

## Context
We need a comprehensive testing strategy that ensures our microservices work correctly in realistic environments, including database interactions, message queue operations, and inter-service communication. Traditional unit tests are insufficient for testing these integration points.

## Decision
We will use Testcontainers for integration testing with the following approach:

- **Testcontainers**: Spin up real containers for testing
- **Database Testing**: Test with real PostgreSQL, MongoDB, Redis
- **Message Queue Testing**: Test with real Kafka, RabbitMQ
- **Service Integration**: Test inter-service communication
- **End-to-End Testing**: Test complete workflows

## Consequences

### Positive
- **Realistic Testing**: Tests run against real infrastructure
- **Confidence**: High confidence that tests reflect production behavior
- **Technology Showcase**: Demonstrates testing best practices
- **Automation**: Tests can be automated in CI/CD pipelines
- **Isolation**: Each test runs in isolated containers
- **Reproducibility**: Tests are reproducible across environments

### Negative
- **Test Execution Time**: Slower than unit tests
- **Resource Usage**: Requires more resources for testing
- **Complexity**: More complex test setup and teardown
- **Dependency**: Tests depend on Docker availability

## Alternatives Considered

1. **Mock Testing**: Faster but less realistic
2. **Embedded Databases**: Simpler but may not reflect production behavior
3. **External Test Environment**: More complex to maintain and coordinate

## Implementation Details

### Testcontainers Configuration
- **Container Lifecycle**: Automatic startup and cleanup
- **Resource Management**: Efficient resource usage
- **Network Configuration**: Isolated network for tests
- **Volume Mounting**: Persistent data when needed
- **Environment Variables**: Configuration for test containers

### Database Testing
- **PostgreSQL**: Test with real PostgreSQL instances
- **MongoDB**: Test with real MongoDB instances
- **Redis**: Test with real Redis instances
- **Data Setup**: Initialize test data in containers
- **Cleanup**: Automatic cleanup after tests

### Message Queue Testing
- **Kafka**: Test with real Kafka cluster
- **RabbitMQ**: Test with real RabbitMQ instances
- **Event Testing**: Test event publishing and consumption
- **Message Verification**: Verify message content and timing

### Service Integration Testing
- **API Testing**: Test REST API endpoints
- **Service Communication**: Test inter-service calls
- **Authentication**: Test with real Keycloak instance
- **Circuit Breakers**: Test resilience patterns

### Test Categories
- **Unit Tests**: Fast tests for business logic
- **Integration Tests**: Tests with real dependencies
- **Contract Tests**: Verify service contracts
- **End-to-End Tests**: Complete workflow testing

### CI/CD Integration
- **Automated Testing**: Run tests in CI/CD pipelines
- **Parallel Execution**: Run tests in parallel for speed
- **Test Reporting**: Generate test reports and coverage
- **Failure Analysis**: Detailed failure information

### Performance Testing
- **Load Testing**: Test under load with real infrastructure
- **Stress Testing**: Test system limits
- **Benchmarking**: Performance benchmarks
- **Resource Monitoring**: Monitor resource usage during tests

### Test Data Management
- **Test Data Generation**: Generate realistic test data
- **Data Cleanup**: Ensure clean state between tests
- **Data Versioning**: Version test data schemas
- **External Data**: Handle external API dependencies

