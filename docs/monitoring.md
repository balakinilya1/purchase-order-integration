# Monitoring & Operations

## KPIs

| KPI | Target / purpose |
|---|---|
| Scheduled runs | 100% expected runs visible |
| Eligible POs | Volume trend |
| Successful SAP POs | End-to-end throughput |
| Failed POs | < 1% target for technical/data failures |
| Processing time | 95% < 10 min |
| Retry count | Detect dependency instability |
| DLQ size | Target 0 unresolved messages |

The thresholds above are portfolio assumptions.

## Alerts

Alert when:

- a scheduled run is missed;
- authentication fails;
- failure rate exceeds 1% in a run;
- DLQ contains messages;
- processing time exceeds 10 minutes for the SLA population.

## Traceability

Every message should carry:

```text
Correlation ID
Salesforce PO ID
SAP Purchase Order number (when created)
Processing timestamp
```
