# ADR-004: CQRS and Event Sourcing for Order Service

## Status
Accepted

## Context
The Order Management Service needs to handle complex order processing workflows, maintain complete audit trails, and support high-performance queries for order status and history. Traditional CRUD approaches may not be sufficient for these requirements.

## Decision
We will implement Command Query Responsibility Segregation (CQRS) and Event Sourcing for the Order Management Service using the following approach:

- **Event Sourcing**: Store all order state changes as events
- **CQRS**: Separate command and query models
- **Axon Framework**: Use Axon for event sourcing implementation
- **Event Store**: PostgreSQL as the event store
- **Read Models**: Separate read models for different query requirements

## Consequences

### Positive
- **Complete Audit Trail**: Every state change is recorded as an event
- **Performance**: Optimized read models for different query patterns
- **Scalability**: Read and write models can be scaled independently
- **Business Intelligence**: Rich event data for analytics
- **Technology Showcase**: Demonstrates advanced data patterns
- **Temporal Queries**: Ability to query data at any point in time

### Negative
- **Complexity**: More complex than traditional CRUD
- **Learning Curve**: Team needs to understand event sourcing concepts
- **Event Schema Evolution**: Managing changes to event schemas
- **Storage Overhead**: Events require more storage than current state

## Alternatives Considered

1. **Traditional CRUD**: Simpler but lacks audit trail and query optimization
2. **Event Sourcing Only**: Without CQRS, would limit query performance
3. **CQRS Only**: Without event sourcing, would lose audit capabilities

## Implementation Details

### Event Sourcing Components
- **Aggregates**: Order aggregate for business logic
- **Commands**: CreateOrder, UpdateOrder, CancelOrder, etc.
- **Events**: OrderCreated, OrderUpdated, OrderCancelled, etc.
- **Event Store**: PostgreSQL with Axon's event store implementation
- **Snapshots**: Periodic snapshots for performance optimization

### CQRS Implementation
- **Command Side**: Handle commands and produce events
- **Query Side**: Build read models from events
- **Read Models**: Optimized views for different query patterns
- **Projections**: Event handlers that build read models

### Axon Framework Features
- **Command Bus**: Handle commands and route to aggregates
- **Event Bus**: Publish events to event store and projections
- **Query Bus**: Handle queries against read models
- **Saga Manager**: Coordinate distributed transactions
- **Event Store**: Persistent storage for events

### Read Models
- **Order Summary**: Basic order information for lists
- **Order Details**: Complete order information with items
- **Order History**: Timeline of order state changes
- **Customer Orders**: Orders grouped by customer
- **Analytics**: Aggregated data for reporting

### Event Schema
```json
{
  "eventId": "uuid",
  "aggregateId": "order-id",
  "eventType": "OrderCreated",
  "timestamp": "2024-01-01T00:00:00Z",
  "data": {
    "customerId": "customer-id",
    "items": [...],
    "totalAmount": 100.00
  }
}
```
