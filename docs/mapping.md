# Purchase Order Mapping

The table below is the portfolio target mapping for the Purchase Order scenario. It is a design artefact and is not extracted from a production system or implementation evidence.

| Salesforce | SAP S/4HANA | Rule |
|---|---|---|
| `PO_Number__c` | External reference / correlation key | Preserve as source business key |
| `Supplier_Code__c` | `Supplier` | Direct mapping after supplier validation |
| `Company_Code__c` | `CompanyCode` | Direct mapping |
| `Purchasing_Org__c` | `PurchasingOrganization` | Direct mapping |
| `Purchasing_Group__c` | `PurchasingGroup` | Direct mapping |
| `Order_Date__c` | Purchase order date | Convert to SAP date format |
| `CurrencyIsoCode` | `DocumentCurrency` | ISO currency code |
| `Items[].Material__c` | `Material` | Direct mapping / validation |
| `Items[].Plant__c` | `Plant` | Direct mapping |
| `Items[].Quantity__c` | `OrderQuantity` | Decimal validation |
| `Items[].UOM__c` | `PurchaseOrderQuantityUnit` | Convert only if agreed |
| `Items[].Net_Price__c` | `NetPriceAmount` | Decimal + currency validation |
| SAP `PurchaseOrder` | `SAP_Purchase_Order__c` | Write returned SAP number to Salesforce |

## Validation

Before SAP call:

- supplier exists / is valid;
- company code and purchasing organization are allowed;
- at least one item exists;
- quantity > 0;
- currency and UoM are valid;
- source PO has not already been processed.

Exact Salesforce field names and the final SAP payload must be confirmed against the real schemas before implementation.
