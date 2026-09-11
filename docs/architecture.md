# Solution Architecture

## Context

Salesforce owns the source Purchase Order record. SAP S/4HANA is the system of record for the ERP Purchase Order. SAP Integration Suite provides orchestration, transformation, connectivity and operational control.

## Logical flow

```text
Timer
  ↓
Salesforce query
  ↓
Validate / filter
  ↓
Map Salesforce → S/4HANA
  ↓
Create Purchase Order
  ↓
Read SAP PO number
  ↓
Update Salesforce
```

## Components

| Component | Responsibility |
|---|---|
| Salesforce | Store and expose eligible Purchase Orders; receive SAP PO reference |
| Cloud Integration | Scheduling, validation, mapping, routing, retry and monitoring |
| SAP S/4HANA | Create and return Purchase Order |
| JMS queue | Optional asynchronous retry boundary for receiver failures |

## Non-functional targets — portfolio assumptions

- 99.9% monthly integration availability
- 95% of eligible POs completed within 10 minutes after the scheduled run
- ~500 POs/day; peak ~100 POs/hour
- No duplicate SAP PO creation during retry/recovery

These targets are deliberately assumptions for the case study, not claims about the source mission.
