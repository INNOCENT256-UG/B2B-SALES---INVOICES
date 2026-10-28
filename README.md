 **Project status:** Portfolio prototype. Headline metrics have been checked against the cleaned source CSV. Complete browser-based interaction testing and a final usability review before describing this as production-ready.

## Overview

This project turns invoice-line data into a business-facing dashboard. It is designed to help users explore sales performance, understand gross profitability, compare customer and product contributions, and review shipping duration.

## Architecture
Single file, split into marked layers:
- **Data**: `D`, the cleaned CSV, dictionary-encoded (customers/products/dates stored once, rows reference them by index). Nothing was altered or invented.
- **Logic** (`//<LOGIC>` block): `filterRows`, `agg` (all KPI math in one place), `groupBy`, `lag`, `weekKey`. Pages never re-implement metrics.
- **Presentation**: one function per page (`ov`, `sales`, `cust`, `prod`, `ship`), a generic `table()` (search + sort) and `mk()` for charts.

Deviation from the brief: the requested React/TypeScript/Tailwind project isn't built here; this environment publishes a self-contained page. The layering above maps directly onto a React port (`logic` → `lib/metrics.ts`, page functions → components).

## Data assessment
- 8,000 rows × 15 columns; no nulls, no duplicate rows, no duplicate (invoice, product) pairs.
- **Unit of observation = invoice line.** 584 distinct invoices (avg 13.7 lines). Each invoice has exactly one customer, order date and ship date, so invoice-level metrics are safe. invoice_no 139 is absent (gap in numbering, not investigated further).
- `revenue = quantity × unit_price`, `cost = quantity × unit_cost`, `margin = revenue − cost` (all verified to rounding). So margin **is** gross profit: $1,199,078.37 on $4,122,067.37 revenue (29.09%). All margins are positive.
- Order dates: 2026-07-30 → 2026-08-19 (15 order days, weekdays only). Ship dates run to 2026-09-03. No ship date precedes its order date.

## KPI definitions
Revenue = Σ revenue. Cost = Σ cost. Gross Profit = Revenue − Cost. Gross Margin % = GP ÷ Revenue × 100 (shown "–" if revenue is 0). Invoices/Customers/Products = distinct invoice_no / customer_id / product_id. Avg Revenue per Invoice = revenue ÷ distinct invoices (valid because an invoice belongs to one customer). Days to ship = ship_date − order_date, per invoice.

## Validation performed
The dashboard's own `filterRows`/`agg` code was extracted and run in Node against pandas: totals, distinct counts, a combined date+category+segment filter (revenue 287,610.16, cost 208,378, 56 invoices, 48 customers, 393 lines), both boundary dates (inclusive), an empty result, and average days to ship (3.755) all matched exactly. **Not yet tested:** visual rendering in a browser, mobile/tablet layout, and chart interactions. Please open the page and review these yourself.

## Known limitations
- **Only ~3 weeks of data**: no year-over-year, no reliable period-over-period, no seasonality. Weekly view marks partial weeks (*).
- **Segment varies within a customer (287 customers) and within an invoice (524)**, so it is a line-level attribute, not a customer attribute. The segment filter filters lines. Its business meaning (segA–segD) should be confirmed.
- 2 customer names map to 2 IDs each; 29 product names map to 2 IDs each. The dashboard keys on IDs and shows "#ID" for ambiguous product names. Whether these are true duplicates needs a business answer.
- unit_price varies 1.2–1.7× within a product_id (cost doesn't); no price history exists to explain it.
- Large single lines exist (max 767 units, $58k); 131 lines exceed 100 units. They are kept as-is.
- No promised/expected ship date, so nothing is called "late".

## Future improvements
Export filtered tables to CSV; more history for trends; customer/product master data to resolve ID/name conflicts; React/TypeScript port with unit tests; Project 1 pipeline output feeding the dashboard automatically.


### Dashboard sections

- **Overview** — revenue, cost, gross profit, gross margin, invoice/customer/product counts, units sold, and category performance.
- **Sales Performance** — sales and profitability trends over the available order-date range.
- **Customers** — customer-level performance and comparisons.
- **Products** — product and category performance.
- **Orders & Shipping** — order-level summaries and shipping-duration analysis.

### Verified headline metrics

The figures below were calculated from the cleaned source dataset and compared with the data embedded in the dashboard.

| Metric | Value |
|---|---:|
| Invoice-line records | 8,000 |
| Revenue | $4,122,067.37 |
| Cost | $2,922,989.00 |
| Gross profit | $1,199,078.37 |
| Gross margin | 29.09% |
| Distinct invoices | 584 |
| Distinct customers | 308 |
| Distinct products | 160 |
| Units sold | 88,309 |

**Date coverage:** order dates run from July 30, 2026 through August 19, 2026. Shipping dates extend through September 3, 2026.

These metrics describe the dataset included with this prototype; they should not be interpreted as live business results.

## Business questions this dashboard supports

- How much revenue and gross profit were recorded in the selected period?
- What is the gross margin?
- How do sales and profitability change over time?
- Which customers, segments, categories, or products contribute most?
- How many invoices, customers, products, and units are represented?
- How long did orders take to ship after the order date?

## Technology

- HTML
- CSS
- JavaScript
- Chart.js 4.4.1, loaded from a CDN

This is a standalone HTML prototype. It does not require a framework, build process, or package installation. A modern browser and an internet connection for the Chart.js CDN dependency are required.

## Metric definitions

- **Revenue:** sum of the `revenue` values in the included invoice-line records.
- **Cost:** sum of the `cost` values in the included invoice-line records.
- **Gross profit:** revenue minus cost.
- **Gross margin:** gross profit divided by revenue, multiplied by 100.
- **Units sold:** sum of the `quantity` values.
- **Shipping duration:** calendar-day difference between the order date and ship date.

Gross profit is not the same as net profit. The dataset may not include operating expenses, taxes, or other costs needed to calculate net profit. Shipping duration alone does not show whether an order was late; promised and actual delivery dates would be needed for that assessment.

## Data and privacy

The dashboard embeds its data in [REPORTS][REPORTS/index.html]` so it can run as a standalone prototype. Before publishing this repository publicly, confirm that the records are approved for public sharing. If the data is client-owned, confidential, or contains identifiable customer information, replace it with anonymized or synthetic sample data before making the repository public.

The dashboard does not connect to a live database or automatically refresh from a source system.

## Limitations

- The dashboard is a static HTML/JavaScript prototype, not a deployed production application.
- Chart.js is loaded from a CDN, so an internet connection is needed for charts to render.
- The dashboard uses embedded data; changes to the source CSV will not automatically update it.
- The available order-date range is limited, so it should not be used to make unsupported year-over-year or long-term trend claims.
- Shipping duration is calculated from order date to ship date; delivery lateness cannot be established from the available fields.
- Browser testing of every interaction and a final accessibility/usability review should be completed before calling the dashboard production-ready.

## Possible next improvements

- Test all filters, navigation items, charts, sorting, and table interactions in a browser.
- Add a documented data-refresh workflow.
- Add automated checks that compare dashboard totals against the source dataset.
- Improve accessibility, responsive behavior, and loading/error states.
- Publish a screenshot or short demo GIF after checking the data-sharing permissions.
- Consider a framework or backend only if the project requirements grow beyond this standalone prototype.

## Frequently asked questions

See [`FAQ.md`](FAQ.md) for answers about running the dashboard, its metrics, data privacy, and current limitations.

## License

No license has been specified yet. Unless a license is added, others should not assume they have permission to reuse, modify, or redistribute this project. Add a license only after confirming you have the rights to license the code and any included data.
