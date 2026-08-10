# Project Worksheet

Record reusable identifiers and decisions here. This file is safe for non-secret IDs only.

## Cloud and governance

| Item | Value | Decision owner / evidence |
| --- | --- | --- |
| Google Cloud project name | RR Performance Dashboard | Confirmed in Google Cloud Console |
| Google Cloud Project ID | `rr-performance-dashboard` | Project number `390497740732` |
| Billing account name | My Billing Account (`015B3F-29C42D-F70CA3`) | Linked and active; billed in AUD |
| BigQuery location | Singapore (`asia-southeast1`) | Fixed for all dashboard datasets and transfers |
| Cloud Run region | Singapore (`asia-southeast1`) | Keep compute beside BigQuery |
| Monthly budget amount | AUD 50 | Alerts at 20%, 50%, 90% and 100%; budget ID `b4995692-0211-49b8-a661-35b1120e729d` |
| Reporting time zone | Asia/Singapore (UTC+8) | Matches the Google Ads account |
| Reporting currency | SGD | Matches the Google Ads account |

## Source identifiers

| Item | Value | Validation |
| --- | --- | --- |
| GA4 Property ID |  | Correct property and `raphandremy.com` stream |
| GA4 Measurement ID |  | Begins with `G-` |
| GA4 BigQuery dataset |  | `analytics_PROPERTY_ID` after export starts |
| Google Ads Customer ID | `778-648-4258` | RAPH&REMY account, not the manager account |
| Search Console property | `sc-domain:raphandremy.com` | Domain property; delegated owner access confirmed |
| Meta Business ID |  | Correct business portfolio |
| Meta Ad Account ID |  | Correct active ad account |
| Meta Pixel / Dataset ID |  | Correct website dataset |
| Meta App ID |  | App belongs to correct business |
| Shopify shop name |  | Text before `.myshopify.com` |
| Shopify Client ID |  | Reporting app installed read-only |

## Reporting definitions

| Definition | Approved rule |
| --- | --- |
| Executive net revenue | Shopify orders less approved refunds and discounts |
| Included order statuses |  |
| Refund treatment | Order-date restatement or refund-date adjustment - decide |
| Default comparison | Previous period and previous year - confirm |
| Google Ads attribution |  |
| Meta attribution |  |
| GA4 attribution |  |
| Paid blended efficiency | Paid spend divided by Shopify revenue - confirm |

## Configured data paths

| Source / layer | Destination or identity | Status |
| --- | --- | --- |
| Google Ads | `raw_google_ads` | Daily BigQuery transfer `Raph Remy Google Ads Daily`; 30-day refresh window; new Google Ads and PMax tables included |
| Google Ads transfer identity | `bq-google-ads-transfer@rr-performance-dashboard.iam.gserviceaccount.com` | Keyless service account; read-only Google Ads access; BigQuery Data Owner on `raw_google_ads` only |
| Google Search Console | `searchconsole_raph_remy` | Bulk export enabled for `sc-domain:raphandremy.com`; first export may take up to 48 hours |
| Meta Ads raw layer | `raw_meta_ads` | Dataset created; source connector pending |
| Shopify raw layer | `raw_shopify` | Dataset created; source connector pending |
| Transformation layer | `analytics_staging` | Dataset created |
| Reporting layer | `analytics_marts` | Dataset created |

## Never record here

Do not add passwords, access tokens, Meta App Secrets, Shopify Client Secrets, private keys, recovery codes or customer personal information.
