# Frequently Asked Questions (FAQ)

## 1. What is this project?

It is an interactive B2B sales dashboard prototype for exploring revenue, cost, gross profit, gross margin, customer and product performance, and order shipping duration.

## 2. Who is it for?

It is intended as a portfolio project and as a demonstration of how invoice data can be presented to business users. It is not currently a production reporting system.

## 3. How do I run it?

Download or clone the repository and open `index.html` in a modern web browser. No build step or package installation is required.

## 4. Do I need Python, Node.js, or Power BI?

No. The current dashboard is built with HTML, CSS, JavaScript, and Chart.js. It does not require Python, Node.js, or Power BI to run.

## 5. Why do I need an internet connection?

Chart.js is loaded from a CDN. The dashboard's charts may not render when offline unless the Chart.js dependency is downloaded and configured locally.

## 6. What dataset does it use?

The prototype includes embedded invoice-line data. The embedded records were compared against the cleaned source CSV for the fields represented in the dashboard.

## 7. What are the headline figures?

The verified totals for the included dataset are:

- Revenue: **$4,122,067.37**
- Cost: **$2,922,989.00**
- Gross profit: **$1,199,078.37**
- Gross margin: **29.09%**
- Invoice-line records: **8,000**
- Distinct invoices: **584**
- Distinct customers: **308**
- Distinct products: **160**
- Units sold: **88,309**

These are dataset-specific figures, not live business results.

## 8. How is gross profit calculated?

Gross profit is calculated as total revenue minus total cost.

## 9. How is gross margin calculated?

Gross margin is calculated as gross profit divided by revenue, multiplied by 100. It should not be confused with markup or net profit margin.

## 10. Does gross profit mean the business made that much net profit?

No. Net profit generally accounts for additional expenses and other items that may not be present in this dataset. The dashboard reports gross profit only.

## 11. Can I tell whether orders were delivered late?

Not reliably. The data includes order and ship dates, but it does not establish promised delivery dates and actual delivery dates. The dashboard can show shipping duration, not confirmed delivery lateness.

## 12. Does the dashboard update automatically when I change the CSV?

No. The current version uses data embedded in `index.html`. Updating the CSV alone will not update the dashboard; the embedded data and relevant calculations would need to be regenerated or the project would need a data-loading workflow.

## 13. Is this dashboard connected to a live database?

No. It is a standalone prototype and does not connect to a live database or business system.

## 14. Is it safe to make this repository public?

Only if the embedded data and code are approved for public sharing. Check for confidential business data, personal information, and client restrictions first. Anonymize or replace sensitive records before making the repository public.

## 15. What are the current limitations?

It is a prototype, uses embedded data, relies on a CDN for Chart.js, and has not been represented as production-ready. All interactions should be tested in a browser, and accessibility and responsive behavior should be reviewed.

## 16. Can I reuse or redistribute the project?

No license is specified yet. Until a license is added, do not assume reuse, modification, or redistribution is permitted. Also ensure you have the rights to share any data included in the repository.

## 17. What should be improved next?

Recommended next steps are to test all filters and charts, improve accessibility and responsive layout, document how the data is refreshed, add repeatable validation checks, and publish screenshots only after confirming data-sharing permissions.
