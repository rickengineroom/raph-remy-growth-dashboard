# Security Policy

## Data and credential boundaries

This repository must never contain access tokens, passwords, private keys, Meta App Secrets, Shopify Client Secrets, recovery codes or downloaded Google service-account keys.

Safe identifiers such as a Google Cloud Project ID, GA4 Property ID, Google Ads Customer ID, Meta Business ID, Meta Ad Account ID, Meta App ID and Shopify shop name may be recorded in `docs/PROJECT_WORKSHEET.md`.

## Runtime authentication

- Local development: Google Application Default Credentials.
- Cloud Run: the attached `dashboard-runtime` service identity.
- Secret values needed at runtime: Google Secret Manager with least-privilege access.
- Browser: read-only API responses containing aggregated metrics only; never credentials, SQL, stack traces or customer-level data.

## Data minimisation

The MVP uses aggregate orders, refunds, products, campaigns, creatives, queries and ecommerce events. It does not ingest Shopify customers or expose customer names, emails, addresses, phone numbers, payment information or order notes.

## Access

The GitHub repository is private. The deployed dashboard must keep unauthenticated access disabled and use Identity-Aware Proxy. Start with the builder and CEO, then add other viewers only after daily refreshes and reconciliations are stable.

## If a secret is exposed

Stop work, revoke or rotate the affected credential in its source platform, remove it from current files and Git history, and verify that logs and deployed revisions do not retain it. Do not reuse the old value.

