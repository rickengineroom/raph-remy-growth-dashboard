# Approved Prototype Audit

## Baseline confirmation

- Working file: `raph-remy-growth-dashboard-prototype.html`
- Untouched backup: `raph-remy-dashboard-prototype-backup.html`
- SHA-256 for both files: `820A580E259F9252AEEAAAAE491AC22CF541961CFCBCF25526A46368BD4D4F23`
- Typography: Inter loaded from Google Fonts.
- View modes: no client-view or analyst-view switch is present.
- Architecture: one self-contained HTML file with inline CSS and JavaScript; Google Fonts is its only external dependency.
- Live calls: none. The prototype contains no `fetch` call and uses no local or session storage.

The working file and backup are byte-identical to the confirmed source file as of repository creation. The backup is not to be edited.

## Dashboard page inventory

| Navigation order | Page key | Visible title | Main content |
| --- | --- | --- | --- |
| 1 | `executive` | Executive summary | Revenue and order KPIs, revenue chart, opportunities, channel contribution and measurement signals |
| 2 | `opportunities` | Opportunities & tests | Searchable/filterable recommendation cards and opportunity review drawer |
| 3 | `paid` | Acquisition performance | Paid KPIs, campaign performance, efficiency and budget actions |
| 4 | `products` | Website & product | Ecommerce funnel, leakage diagnosis and product-family performance |
| 5 | `creative` | Creative performance | Creative KPIs, concept chart, asset performance and test actions |
| 6 | `organic` | Organic search | Organic KPIs and query opportunity table |
| 7 | `health` | Data quality | Source freshness, measurement diagnostics and issue actions |

## Dummy-data map

All current numbers are demonstrations. They are stored in three places inside the working HTML:

1. Hard-coded HTML markup: KPI labels and values, tables, funnels, cards, badges, data-health rows and source-freshness text.
2. `data-base` attributes: selected Executive Summary values that the date-range control scales in the browser.
3. Inline JavaScript: the `opportunities` evidence/action object; `revenue` and `previous` daily arrays; derived order arrays; and the creative-chart data and labels inside `drawCreativeChart()`.

Page labels in `pageMeta` are interface metadata, not live metrics. The current date filter scales only values carrying `data-base`; it does not apply a real date filter to every component. The comparison toggle changes presentation only.

## Preservation rule

No design changes or live-data substitutions should be made until the approved project setup and source reconciliation phases are complete. When connection work begins, create `DATA_CONTRACT.md` before writing API code and map every visible value above to a defined metric, grain, filter and endpoint.

