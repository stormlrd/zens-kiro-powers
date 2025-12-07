# Event-Driven Architecture Patterns

## Pub/Sub Pattern (SNS)
```
Publisher → SNS Topic → Multiple Subscribers
```
**Use for:** Broadcasting events to multiple consumers

## Queue Pattern (SQS)
```
Producer → SQS Queue → Consumer
```
**Use for:** Decoupling services, load leveling

## Fan-Out Pattern
```
Producer → SNS → Multiple SQS Queues → Multiple Consumers
```
**Use for:** Parallel processing of same event

## Dead Letter Queue Pattern
```
Main Queue → Failed Messages → DLQ → Monitoring/Retry
```
**Use for:** Handling poison messages

## Saga Pattern (Step Functions)
```
Start → Service A → Service B → Service C → End
       ↓ Compensate ← Compensate ← Compensate
```
**Use for:** Distributed transactions

## Best Practices
- Use FIFO queues for ordering
- Implement idempotency
- Set appropriate visibility timeouts
- Monitor queue depth
- Use message attributes for filtering
