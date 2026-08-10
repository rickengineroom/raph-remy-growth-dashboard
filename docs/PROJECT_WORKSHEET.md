# Project Worksheet

Record reusable identifiers and decisions here. This file is safe for non-secret IDs only.

## Cloud and governance

| Item | Value | Decision owner / evidence |
| --- | --- | --- |
| Google Cloud project name |  |  |
| Google Cloud Project ID |  |  |
| Billing account name |  |  |
| BigQuery location |  |  |
| Cloud Run region |  |  |
| Monthly budget amount |  |  |
| Reporting time zone |  |  |
| Reporting currency | SGD (confirm) |  |

## Source identifiers

| Item | Value | Validation |
| --- | --- | --- |
| GA4 Property ID |  | Correct property and `raphandremy.com` stream |
| GA4 Measurement ID |  | Begins with `G-` |
| GA4 BigQuery dataset |  | `analytics_PROPERTY_ID` after export starts |
| Google Ads Customer ID |  | Correct account or MCC |
| Search Console property |  | Domain property preferred; owner access confirmed |
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

## Never record here

Do not add passwords, access tokens, Meta App Secrets, Shopify Client Secrets, private keys, recovery codes or customer personal information.

