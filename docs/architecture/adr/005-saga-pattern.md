# ADR-005: SAGA Pattern for Distributed Transactions

## Status
Accepted

## Context
In a microservices architecture, we need to maintain data consistency across multiple services when processing orders that involve inventory updates, payment processing, and notification sending. Traditional ACID transactions are not possible across service boundaries.

## Decision
We will implement the SAGA pattern to manage distributed transactions across the order processing workflow using both choreography and orchestration approaches:

- **Choreography SAGA**: Services communicate through events
- **Orchestration SAGA**: Central coordinator manages the workflow
- **Compensation Actions**: Rollback mechanisms for failed steps
- **Event Sourcing**: Track saga state changes as events

## Consequences

### Positive
- **Data Consistency**: Maintains consistency across distributed services
- **Fault Tolerance**: Handles failures with compensation actions
- **Scalability**: No distributed locks or blocking transactions
- **Technology Showcase**: Demonstrates advanced distributed patterns
- **Audit Trail**: Complete history of saga execution
- **Flexibility**: Can handle complex multi-step workflows

### Negative
- **Complexity**: More complex than traditional transactions
- **Debugging**: Harder to debug distributed workflows
- **Eventual Consistency**: Temporary inconsistencies during saga execution
- **Compensation Logic**: Need to implement rollback mechanisms

## Alternatives Considered

1. **Two-Phase Commit**: Not suitable for microservices due to blocking nature
2. **Eventual Consistency Only**: Simpler but may not meet business requirements
3. **Synchronous Calls**: Would create tight coupling and reduce availability

## Implementation Details

### SAGA Workflow for Order Processing
1. **Create Order** (Order Service)
2. **Reserve Inventory** (Inventory Service)
3. **Process Payment** (Payment Service)
4. **Send Notifications** (Notification Service)
5. **Update Analytics** (Analytics Service)

### Compensation Actions
- **Order Creation**: Cancel order and refund any payments
- **Inventory Reservation**: Release reserved inventory
- **Payment Processing**: Refund payment if already processed
- **Notification**: Send cancellation notification

### Implementation Approaches

#### Choreography SAGA
```java
// Services publish events and react to events
@EventHandler
public void handleOrderCreated(OrderCreatedEvent event) {
    // Reserve inventory
    // Publish InventoryReservedEvent or InventoryReservationFailedEvent
}
```

#### Orchestration SAGA
```java
// Central coordinator manages the workflow
@Component
public class OrderSagaOrchestrator {
    public void processOrder(CreateOrderCommand command) {
        // Coordinate all steps
        // Handle failures and compensation
    }
}
```

### Saga State Management
- **Saga State**: Track current state of the saga
- **Event Sourcing**: Store saga state changes as events
- **Timeout Handling**: Handle saga timeouts
- **Retry Logic**: Retry failed steps with exponential backoff

### Monitoring and Observability
- **Saga Metrics**: Track saga success/failure rates
- **Distributed Tracing**: Trace saga execution across services
- **Saga Dashboard**: Monitor active and completed sagas
- **Alerting**: Alert on saga failures or timeoutsmize database connections
- **Query Performance**: Monitor slow queries
- **Data Growth**: Track storage usage and growth