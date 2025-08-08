# Architecture Decision Records (ADR)

This directory contains Architecture Decision Records (ADRs) for the E-Commerce Microservices project. ADRs document significant architectural decisions, their context, and rationale to help developers understand why certain choices were made.

## What are ADRs?

Architecture Decision Records are short text documents that capture important architectural decisions made during the project. Each ADR describes:
- The decision that was made
- The context and problem it addresses
- The consequences and trade-offs
- The alternatives that were considered

## ADR Format

Each ADR follows this structure:
- **Title**: Clear, descriptive title
- **Status**: Proposed, Accepted, Deprecated, Superseded
- **Context**: The problem or situation that led to this decision
- **Decision**: The architectural decision that was made
- **Consequences**: The results, both positive and negative
- **Alternatives**: Other options that were considered

## ADR List

- [ADR-001: Microservices Architecture Pattern](./001-microservices-architecture.md)
- [ADR-002: Spring Boot as Primary Framework](./002-spring-boot-framework.md)
- [ADR-003: Event-Driven Architecture with Kafka](./003-event-driven-architecture.md)
- [ADR-004: CQRS and Event Sourcing for Order Service](./004-cqrs-event-sourcing.md)
- [ADR-005: SAGA Pattern for Distributed Transactions](./005-saga-pattern.md)
- [ADR-006: Keycloak for Authentication and Authorization](./006-keycloak-auth.md)
- [ADR-007: Multi-Database Strategy](./007-multi-database-strategy.md)
- [ADR-008: Prometheus and Grafana for Observability](./008-prometheus-grafana.md)
- [ADR-009: Docker and Kubernetes for Deployment](./009-docker-kubernetes.md)
- [ADR-010: Testcontainers for Integration Testing](./010-testcontainers.md)

## How to Create New ADRs

1. Create a new markdown file with the next sequential number
2. Follow the ADR template structure
3. Update this README with the new ADR entry
4. Commit the ADR with a descriptive message

## References

- [ADR GitHub Repository](https://github.com/joelparkerhenderson/architecture_decision_record)
- [ADR Template](https://github.com/joelparkerhenderson/architecture_decision_record/blob/main/adr_template.md)
