# Error Handling & Idempotency

## Error classes

| Type | Example | Action |
|---|---|---|
| Transient | timeout, 5xx, temporary unavailability | Retry |
| Authentication | expired/invalid credential | Fail + alert |
| Business | invalid supplier, missing mandatory data | No retry; DLQ/reprocess |
| Partial completion | SAP PO created, Salesforce update failed | Reconcile before retry |

## Retry policy — portfolio assumption

The integration uses a 3-attempt retry policy for transient technical failures,
with exponential backoff: approximately 1 min → 5 min → 15 min.

JMS queues can be used as a persistence and retry mechanism for temporary
receiver failures in SAP Cloud Integration.

## Dead-letter / reprocessing

The following is the proposed portfolio design for failed message handling:

Main flow
   ↓ technical error
JMS retry
   ↓ after retry limit
PO.DLQ
   ↓
Support review
   ↓
Manual reprocess

The `PO.DLQ` is a logical design concept for this portfolio scenario.
The exact implementation depends on the selected SAP Cloud Integration
retry/JMS configuration and the tenant capabilities.
