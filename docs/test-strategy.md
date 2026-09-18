# Test Strategy

| ID | Scenario | Expected result |
|---|---|---|
| T01 | One valid PO | SAP PO created; Salesforce updated |
| T02 | No eligible POs | Flow ends normally |
| T03 | Multiple POs | All eligible records processed |
| T04 | Missing supplier | Validation error; no SAP PO |
| T05 | SAP timeout | Retry according to policy |
| T06 | SAP 4xx business error | No retry; DLQ/reprocess |
| T07 | SAP PO created, Salesforce update fails | Recovery does not create duplicate SAP PO |
| T08 | Duplicate source PO | Existing SAP reference reused / creation skipped |
| T09 | Authentication failure | Alert + controlled failure |
| T10 | Peak load | 100 POs/hour remains within SLA |

## Acceptance

A successful test run should provide Salesforce PO ID, SAP PO number, correlation ID and execution timestamp.
