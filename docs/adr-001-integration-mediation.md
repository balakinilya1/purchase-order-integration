# ADR-001: SAP Integration Suite as Mediation Layer

**Status:** Accepted

## Decision

Use SAP Integration Suite / Cloud Integration between Salesforce and SAP S/4HANA.

## Why

- decouples the two data models;
- centralizes transformation;
- centralizes credentials and connectivity;
- provides one monitoring and recovery boundary;
- allows the polling design to evolve later without changing the business systems directly.

## Trade-off

The middleware becomes a critical integration component and requires operational ownership.
