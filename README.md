 **Project status:** Portfolio prototype. Headline metrics have been checked against the cleaned source CSV. Complete browser-based interaction testing and a final usability review before describing this as production-ready.

## Overview

This project turns invoice-line data into a business-facing dashboard. It is designed to help users explore sales performance, understand gross profitability, compare customer and product contributions, and review shipping duration.

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

## Run locally

1. Clone or download this repository.
2. Open `index.html` in a modern web browser.
3. Use the dashboard navigation and available filters to explore the data.

For example, using Git:

```bash
git clone https://github.com/<your-username>/b2b-sales-intelligence-dashboard.git
cd b2b-sales-intelligence-dashboard
```

Replace `<your-username>` with the GitHub account that owns the repository, then open `index.html` in your browser.

## Metric definitions

- **Revenue:** sum of the `revenue` values in the included invoice-line records.
- **Cost:** sum of the `cost` values in the included invoice-line records.
- **Gross profit:** revenue minus cost.
- **Gross margin:** gross profit divided by revenue, multiplied by 100.
- **Units sold:** sum of the `quantity` values.
- **Shipping duration:** calendar-day difference between the order date and ship date.

Gross profit is not the same as net profit. The dataset may not include operating expenses, taxes, or other costs needed to calculate net profit. Shipping duration alone does not show whether an order was late; promised and actual delivery dates would be needed for that assessment.

## Data and privacy

The dashboard embeds its data in `index.html` so it can run as a standalone prototype. Before publishing this repository publicly, confirm that the records are approved for public sharing. If the data is client-owned, confidential, or contains identifiable customer information, replace it with anonymized or synthetic sample data before making the repository public.

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
