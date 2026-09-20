# API Design

## Salesforce

**Portfolio assumption:** a custom Salesforce object `Purchase_Order__c` is used. Salesforce REST API resources support query and sObject CRUD operations; the exact object name must be confirmed in the target org.

```text
GET  /services/data/vXX.X/query/?q=<SOQL>
PATCH /services/data/vXX.X/sobjects/Purchase_Order__c/{Id}
```

Example query:

```sql
SELECT Id, PO_Number__c, Supplier_Code__c, Company_Code__c,
       Purchasing_Org__c, Purchasing_Group__c, CurrencyIsoCode,
       SAP_Purchase_Order__c, Integration_Status__c
FROM Purchase_Order__c
WHERE Integration_Status__c = 'Ready'
  AND SAP_Purchase_Order__c = NULL
```

`vXX.X` and field names are intentionally environment-specific placeholders.

## SAP S/4HANA

Use the standard **Purchase Order API** where supported:

```text
POST /sap/opu/odata/sap/API_PURCHASEORDER_PROCESS_SRV/A_PurchaseOrder
```

For an applicable SAP S/4HANA release, the integration can use the standard Purchase Order API, such as API_PURCHASEORDER_PROCESS_SRV (OData V2) or the corresponding current Purchase Order API version.

SAP documents this API for Purchase Order integration; communication scenario **SAP_COM_0053** is associated with the API in SAP documentation.

## API principles

- HTTPS only.
- OAuth/client credentials or the SAP-supported technical authentication mechanism.
- Credentials stored in Security Material.
- API version and endpoint externalized per environment.
- Correlation ID propagated through the flow.
