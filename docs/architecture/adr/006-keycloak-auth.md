# ADR-006: Keycloak for Authentication and Authorization

## Status
Accepted

## Context
A robust authentication and authorization system is required to secure all microservices, support OAuth2/OpenID Connect, enable single sign-on, and provide centralized identity management. The solution should support both user and service authentication, role-based access control (RBAC), and easy integration with Spring Security.

## Decision
We will use **Keycloak** as the identity and access management (IAM) solution for authentication and authorization across all services.

- **OAuth2/OpenID Connect**: Standards-based authentication and authorization
- **JWT Tokens**: Stateless, signed tokens for service-to-service and user authentication
- **RBAC**: Role-based access control for fine-grained permissions
- **Centralized Identity**: Single source of truth for users, roles, and clients
- **Spring Security Integration**: Native support for Spring Boot microservices

## Consequences

### Positive
- **Standards Compliance**: Implements OAuth2 and OpenID Connect
- **Centralized Management**: Unified user, client, and role management
- **Scalability**: Supports large numbers of users and clients
- **Integration**: Easy integration with Spring Security and other frameworks
- **Extensibility**: Supports custom authentication flows and user federation

### Negative
- **Learning Curve**: Keycloak has a complex UI and configuration
- **Operational Overhead**: Requires additional infrastructure and monitoring
- **Single Point of Failure**: Outage impacts all authentication
- **Configuration Complexity**: Requires careful setup for security and multi-tenancy

## Alternatives Considered

1. **Spring Security OAuth2**: Simpler, but lacks advanced features and UI
2. **Auth0**: Cloud-based, but introduces external dependency and cost
3. **Custom Implementation**: More control, but high security risk and maintenance burden

## Implementation Details

- **Keycloak Realm**: Create a dedicated realm for the e-commerce application
- **Clients**: Register each microservice and frontend as a Keycloak client
- **Users & Roles**: Define user groups (e.g., customer, admin) and roles for RBAC
- **OAuth2 Flows**: Use Authorization Code flow for web apps, Client Credentials for service-to-service
- **JWT Validation**: Each service validates JWT tokens using Spring Security's resource server support
- **Role Mapping**: Map Keycloak roles to Spring Security authorities for method and endpoint protection
- **Token Management**: Configure token lifetimes, refresh, and revocation as needed
- **User Federation**: Optionally integrate with external user stores (LDAP, social login)
- **Audit Logging**: Enable Keycloak audit logs for authentication events
