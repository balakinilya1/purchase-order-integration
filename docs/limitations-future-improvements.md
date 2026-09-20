# Limitations & Future Improvements

## Current limitations

- Salesforce object and fields are portfolio assumptions.
- SAP API choice assumes an S/4HANA release where the standard Purchase Order API is available.
- Volumes and SLA are design assumptions.
- No real credentials or runtime evidence are included.

## Future evolution

1. Replace polling with an event-driven trigger if Salesforce business latency requires it.
2. Introduce centralized API management if additional consumers appear.
3. Add automated reconciliation between Salesforce and SAP.
4. Add CI/CD and automated regression tests for the integration artifact.
