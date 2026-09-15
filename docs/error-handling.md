# Error Handling & Idempotency

## Error classes

| Type | Example | Action |
|---|---|---|
| Transient | timeout, 5xx, temporary unavailability | Retry |
| Authentication | expired/invalid credential | Fail + alert |
| Business | invalid supplier, missing mandatory data | No retry; DLQ/reprocess |
| Partial completion | SAP PO created, Salesforce update failed | Reconcile before retry |

## Retry policy — portfolio assumption

**3 attempts** with exponential backoff: approximately **1 min → 5 min → 15 min**.

For Cloud Integration, JMS queues are a suitable persistence/retry mechanism for temporary receiver failures. SAP documents JMS-based retry and dead-letter handling.

## Dead-letter / reprocessing

Design:

```text
Main flow
   ↓ error
JMS retry
   ↓ after retry limit
PO.DLQ
   ↓
Support review
   ↓
Fix data / dependency
   ↓
Manual reprocess
```

**DLQ rule:** messages that cannot be completed after the defined retry policy are retained for controlled reprocessing. The exact platform configuration must follow the tenant's available JMS/retry capabilities.

## Idempotency

Use a stable key: `Salesforce Purchase_Order__c.Id`. Before creating a PO, check whether `SAP_Purchase_Order__c` is already populated. For stronger protection, persist a processing key such as `SF-{SalesforceId}` and use the same key across retries.

The architecture must not rely on “exactly once” behaviour from middleware alone; receiver-side duplicate protection is also required for end-to-end safety. SAP documentation explicitly highlights idempotency when JMS retry is used.
