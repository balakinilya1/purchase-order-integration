# Business Requirements

## Functional

| ID | Requirement |
|---|---|
| BR-01 | Query eligible Purchase Orders from Salesforce on a schedule. |
| BR-02 | Stop processing cleanly when no eligible POs are returned. |
| BR-03 | Validate mandatory data before calling SAP. |
| BR-04 | Transform Salesforce PO data into the SAP S/4HANA Purchase Order structure. |
| BR-05 | Create the Purchase Order in SAP S/4HANA. |
| BR-06 | Return the created SAP PO number to Salesforce. |
| BR-07 | Mark the source record as processed only after successful SAP creation. |
| BR-08 | Support safe retry and manual reprocessing. |

## Eligibility rule — portfolio assumption

A Salesforce PO is eligible when:

```text
Integration_Status__c = 'Ready'
AND
SAP_Purchase_Order__c is empty
```

The exact Salesforce object/field names are assumptions and must be replaced by the real data model.

## Operational assumptions

- Schedule: every 15 minutes.
- Average daily volume: 500 POs.
- Peak: 100 POs/hour.
- SLA: 95% completed within 10 minutes after the run.
- Technical retry: 3 attempts.
- Business/data errors: no automatic retry.
