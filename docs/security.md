# Security

## Design

- Salesforce: OAuth-based technical integration user.
- SAP S/4HANA: technical communication user / supported API authentication.
- Credentials: SAP Integration Suite Security Material.
- Transport: HTTPS/TLS.
- GitHub: no credentials, tokens or payloads containing sensitive data.

## Access

Least privilege:

- Salesforce integration user: read Purchase Orders + update only integration status/reference fields.
- SAP technical user: create Purchase Orders through the required API only.
- Integration developers: no production secrets in source control.

## Logging

Do not log full Purchase Order payloads by default. Log identifiers, status, error category and correlation ID. Enable payload logging temporarily for controlled troubleshooting only.
