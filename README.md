# Raph & Remy Growth Dashboard

Private ecommerce performance dashboard for Raph & Remy. The approved visual prototype will be connected to GA4, Google Ads, Search Console, Meta Ads and Shopify through BigQuery, a read-only Node.js API and a private Google Cloud Run service.

## Current status

Repository foundation is complete. No live data integration has started.

- Approved prototype preserved as `raph-remy-growth-dashboard-prototype.html`.
- Untouched byte-identical backup preserved as `raph-remy-dashboard-prototype-backup.html`.
- Seven dashboard pages inventoried in `docs/PROTOTYPE_AUDIT.md`.
- The seven-phase implementation is mapped in `docs/BUILD_PLAN.md`.
- Safe project identifiers and governance decisions can be recorded in `docs/PROJECT_WORKSHEET.md`.
- The source guide is retained under `docs/reference/`.

## Preview the approved prototype

The file can be opened directly in a browser. For a local web preview from the repository root:

```powershell
python -m http.server 4173
```

Then open:

`http://127.0.0.1:4173/raph-remy-growth-dashboard-prototype.html`

## Build order

1. Prepare the cloud project, budget, access and shared BigQuery location.
2. Connect and reconcile GA4, Google Ads and Search Console.
3. Connect and reconcile Meta Ads.
4. Connect and reconcile Shopify.
5. Define metrics, inspect real schemas and build tested BigQuery views.
6. Add the private API and replace dummy data one page at a time.
7. Deploy privately to Cloud Run with Identity-Aware Proxy.

The gates and deliverables for each phase are in `docs/BUILD_PLAN.md`. Work stops at the first failed checkpoint; source setup, modelling, API work and interface work are not collapsed into one step.

## Security rules

- Never commit or paste secrets, tokens, passwords or service-account JSON keys.
- Use Google Application Default Credentials locally and a Cloud Run service identity in production.
- Store Meta and Shopify secrets in a password manager during setup and Google Secret Manager when the service needs them.
- Keep customer names, emails, addresses, phone numbers and order notes out of the analytics datasets and dashboard.
- Keep the GitHub repository and deployed dashboard private.

See `SECURITY.md` for the full repository policy.

