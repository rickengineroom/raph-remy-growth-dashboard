# Raph & Remy Dashboard Build Plan

## Working method

The project follows four action types from the approved guide:

- **You:** perform account, authorization and governance actions in the named platform.
- **Codex:** inspect or change the repository after the relevant inputs exist.
- **Wait:** allow managed transfers to create or refresh data without rebuilding them prematurely.
- **Check:** reconcile the result before advancing.

One phase is active at a time. A phase is complete only when every exit gate passes. No secrets or customer-level personal data are placed in chat, source control or browser responses.

## Phase 0 - Repository baseline

**Status:** Complete.

**Outcome:** A private, reversible project foundation that preserves the approved interface.

**Deliverables**

- Approved prototype and untouched byte-identical backup.
- Prototype page inventory and dummy-data map.
- Source guide retained in `docs/reference/`.
- Project worksheet, security policy and gated build plan.

**Exit gate**

- Exact prototype filename confirmed.
- Backup hash matches the working prototype hash.
- Seven dashboard pages documented without changing the design.

## Phase 1 - Prepare

**Owner:** You for account and cloud-console actions; Codex for repository support and validation checklists.

**Outcome:** Approved project, cost controls, permissions and BigQuery structure.

**Tasks**

1. Confirm access to Google Cloud, GA4, Google Ads, Search Console, Meta and Shopify; ensure required 2-Step Verification and owner roles.
2. Make and record the BigQuery location governance decision before creating datasets.
3. Select or create the approved Google Cloud project and confirm active billing.
4. Create the dashboard build budget and alerts at 20%, 50%, 90% and 100% of the agreed monthly amount.
5. Enable BigQuery, BigQuery Storage, BigQuery Data Transfer, Cloud Run, Cloud Build, Artifact Registry, Secret Manager and Identity-Aware Proxy APIs.
6. Create `raw_google_ads`, `raw_meta_ads`, `raw_shopify`, `analytics_staging` and `analytics_marts` in the same location.
7. Fill the safe identifiers and decisions in `docs/PROJECT_WORKSHEET.md`.

**Exit gate**

- All six source/platform access checks pass.
- BigQuery location and decision owner are recorded.
- Billing is active, budget alerts exist and every required API is enabled.
- All five datasets exist in the one approved location.

## Phase 2 - Google data

**Outcome:** GA4, Google Ads and Search Console refresh into BigQuery and reconcile with their source interfaces.

**Tasks**

1. Validate GA4 ecommerce events (`view_item`, `add_to_cart`, `begin_checkout`, `purchase`) and ensure purchase IDs, values, currency and item arrays are correct and not duplicated.
2. Enable daily GA4 BigQuery export; wait up to 24 hours for the first `events_YYYYMMDD` table.
3. Create the standard Google Ads managed transfer with a 30-day refresh window and Performance Max tables when applicable; backfill only after the first run succeeds.
4. Confirm verified ownership of the complete Search Console property, grant the Google-managed export identity its required BigQuery roles and enable bulk export; wait up to 48 hours for first tables.
5. Compare a completed date or period against each source using the same account, time zone, currency and attribution settings.

**Exit gate**

- GA4 daily table exists and validated ecommerce events are present.
- Google Ads transfer succeeds, spend reconciles and required history is loaded.
- Search Console export log and both impression tables exist; clicks reconcile.

## Phase 3 - Paid social

**Outcome:** Controlled Meta Ads data refreshes into `raw_meta_ads` and reconciles without double counting.

**Tasks**

1. Record the safe Meta business, ad-account, pixel/dataset and app identifiers.
2. Create the business reporting app; keep the App Secret in the password manager.
3. Configure the Facebook Ads managed transfer, its generated OAuth redirect URI, the approved object/action collections, ad-level daily grain and 30-day refresh window.
4. Start without placement or device breakdowns; add those only in a separate model after core ad-level totals reconcile.
5. Compare spend, purchases and purchase value with the same attribution view and schedule token reauthorization for day 50.

**Exit gate**

- Latest transfer run succeeds and required raw tables contain rows.
- Spend and purchase value reconcile within an explained tolerance.
- Meta attribution definition and day-50 renewal reminder are recorded.

## Phase 4 - Commerce

**Outcome:** Read-only Shopify orders, refunds and products refresh into `raw_shopify`; Shopify net revenue becomes the executive source of truth.

**Tasks**

1. Confirm the `.myshopify.com` shop name, store currency and time zone.
2. Create the reporting app in Shopify's Dev Dashboard with read-only scopes only; never request customer data for the MVP.
3. Create the managed Shopify transfer for orders, transactions, refunds/returns, products/variants and approved operational objects.
4. Reconcile a completed seven-day period for order count, gross sales, discounts, refunds and net revenue.
5. Document test/cancelled/unpaid order exclusions and refund-date treatment.

**Exit gate**

- Shopify transfer succeeds and the required raw tables contain rows.
- Orders and net revenue reconcile for seven completed days.
- Revenue, status and refund rules are approved in the worksheet.

## Phase 5 - Model

**Outcome:** Every visible prototype component has a data contract and every dashboard mart is backed by tested, reconciled BigQuery SQL.

**Tasks**

1. Create `DATA_CONTRACT.md` without changing the approved design. Inventory every metric, chart, table, filter and opportunity card with dummy-data location, required grain, filter inputs and endpoint.
2. Export actual `INFORMATION_SCHEMA.COLUMNS` results for every raw source. Do not guess connector table or column names.
3. Resolve definition questions for Shopify net revenue, order status, refunds, reporting time zone/currency and each platform's attribution.
4. Build idempotent SQL under `sql/`: source staging views first, then executive summary, paid, creative, product funnel, organic search, opportunities and data-health marts.
5. Add safe division, explicit grains, date/source filters and duplicate/nonnegative/reconciliation tests.
6. Run SQL in documented order, review bytes processed and stop at the first error.

**Exit gate**

- Data contract maps every dummy value to a defined future source.
- Real schemas, not assumed columns, drive the SQL.
- All SQL and duplicate-grain tests pass.
- Shopify revenue and paid-platform spend reconcile over the same completed period.

## Phase 6 - Connect

**Outcome:** A production-ready private Node.js service reads BigQuery marts, while local mock mode preserves easy visual preview.

**Planned API routes**

| Route | Primary mart |
| --- | --- |
| `/api/executive-summary` | `mart_executive_summary` |
| `/api/paid-performance` | `mart_paid_performance` |
| `/api/creative-performance` | `mart_creative_performance` |
| `/api/products` | `mart_product_funnel` |
| `/api/organic-search` | `mart_organic_search` |
| `/api/opportunities` | `mart_opportunities` |
| `/api/data-health` | `mart_data_health` |

**Tasks**

1. Build with `@google-cloud/bigquery` and Application Default Credentials; never use a downloaded service-account key.
2. Validate inclusive date ranges and source filters, use parameterized queries, cap result sizes and return `last_refreshed`.
3. Add automated route and mapping tests plus loading, empty, error/retry and freshness states.
4. Connect only Executive Summary first. Reconcile seven completed days and test responsive and failure states.
5. Connect Paid, Creative, Products, Organic, Opportunities and Data Health in that order, advancing only when the previous page passes.
6. Run the full test suite and production build; inspect for dummy values, secrets and broken routes.

**Exit gate**

- Every page handles loading, empty, error/retry and freshness states.
- Navigation, completed-date filters, responsive layout and accessibility checks pass.
- No dummy metrics or secret/customer data remains in live mode.

## Phase 7 - Launch

**Outcome:** A private Cloud Run dashboard with controlled viewer access and an operating routine.

**Tasks**

1. Create `dashboard-runtime` with BigQuery Job User and the minimum necessary Data Viewer access; create no key.
2. Confirm the app listens on `process.env.PORT` and its production start command works.
3. Prepare and review a source-deployment command for service `raph-remy-growth-dashboard`, the approved project/region and runtime identity, with unauthenticated access disabled and IAP enabled.
4. Deploy only after explicit approval and test approved and unapproved Google sessions.
5. Record the access list, budget checks, transfer alerts, weekly reconciliation and Meta token-renewal routine.

**Exit gate**

- IAP is enabled; approved users can sign in and unapproved users cannot load the dashboard.
- All five source refreshes, SQL tests, interface states, security checks and cost controls pass.
- Several daily refreshes complete without unexplained reconciliation differences before client access is considered.

## Post-launch backlog

Only after the live foundation is stable:

1. Add transparent, deterministic opportunity rules with evidence, date range, minimum sample, confidence and suggested action.
2. Add an A/B test register with predeclared primary and guardrail metrics; never call a winner before minimum sample passes.
3. Consider historical Search Console loading and advanced attribution.
4. Consider provider-neutral AI analysis over aggregated mart data only. AI may explain evidence and draft investigations; it must not change budgets, launch ads or replace source-of-truth metrics.

## Immediate next checkpoint

Begin Phase 1 with the BigQuery location decision and the six-platform access check. Do not start API or SQL implementation until the managed sources have refreshed and reconciled.

