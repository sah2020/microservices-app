# Service Startup Guide

This guide explains how to start all microservices for local development and testing. For environment setup, prerequisites, and migration tools, see the [Development Environment Setup](./development-environment.md).

## Starting All Services with Docker Compose

1. Ensure Docker Desktop is running and all prerequisites are met.
2. Navigate to the infrastructure directory:
   ```bash
   cd infrastructure/docker-compose
   ```
3. Start all infrastructure and service containers:
   ```bash
   docker-compose up -d
   ```
4. Check the status of all containers:
   ```bash
   docker-compose ps
   ```
5. Access service endpoints as described in the main [README.md](../../README.md).

## Starting Services Individually (Development Mode)

1. Ensure all infrastructure services (databases, Kafka, RabbitMQ, etc.) are running via Docker Compose.
2. In a new terminal, navigate to the service directory (e.g., `user-service/`).
3. Start the service using Maven:
   ```bash
   mvn spring-boot:run
   ```
4. Repeat for each service you want to run locally.

## Common Startup Issues

- **Port Conflicts**: Ensure no other processes are using the required ports (see README for port assignments).
- **Database Connection Errors**: Verify that the database containers are running and accessible.
- **Configuration Issues**: Check that environment variables and configuration files are set up correctly.
- **Migration Failures**: See the [Development Environment Setup](./development-environment.md#11-database-migration-tools) for migration troubleshooting.

For more troubleshooting tips, see the [Development Environment Setup](./development-environment.md#troubleshooting) section.
