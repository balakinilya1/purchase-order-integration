# Mission Evidence vs Portfolio Design

## What the supplied PDF actually shows

The SAP Discovery Center material is titled **“Synchronize Orders Data Between SAP S/4HANA and Third-Party CRM”** and shows:

- Salesforce as the CRM side;
- SAP S/4HANA as the ERP side;
- SAP Cloud Integration as the mediation layer;
- scheduled polling with Timer Start;
- query of Orders from Salesforce;
- transformation to SAP format;
- creation of a Sales Order in SAP S/4HANA;
- transformation of the SAP response;
- update of Salesforce with the SAP Sales Order ID.

The PDF also contains a red note that the Timer configuration was not performed because credentials were unavailable, and another note that monitoring verification was not repeated because it had already been done in the previous Business Partner Synchronization project.

## Portfolio adaptation

For this repository, the business object is **Purchase Order**, as defined by the project scope. The following are therefore portfolio design decisions rather than evidence from the mission:

- Purchase Order data model;
- Salesforce `Purchase_Order__c` example;
- SAP Purchase Order API;
- field-level mapping;
- 15-minute schedule;
- 500 POs/day and 100 POs/hour;
- 99.9% availability / 10-minute processing SLA;
- 3 retries and DLQ/reprocessing;
- detailed validation and idempotency rules.

This distinction is intentional: the repository demonstrates architecture thinking without claiming hands-on execution that did not happen.
