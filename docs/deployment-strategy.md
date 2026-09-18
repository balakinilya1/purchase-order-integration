# Deployment Strategy

## Environments

```text
DEV → TEST → PROD
```

Promote the same integration artifact; keep environment-specific configuration outside the artifact where possible.

## Externalized configuration

- Salesforce base URL
- SAP base URL
- credential aliases
- schedule
- retry parameters
- logging level

## Deployment checklist

- [ ] Security material available
- [ ] Salesforce connection tested
- [ ] SAP API connection tested
- [ ] Mapping validated
- [ ] Retry/DLQ configuration checked
- [ ] Monitoring/alerts enabled
- [ ] Rollback/reprocessing procedure agreed
