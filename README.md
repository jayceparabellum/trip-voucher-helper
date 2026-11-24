# Trip Voucher Helper

Tools and a standard process for field technicians finishing a work trip's expense report (voucher) in Unanet. The repo has three parts:

1. **The app**: a single-page chat helper that answers process questions, turns receipts into lossless PNGs, checks every line, builds the one PDF for the report, and keeps your trip trackers up to date.
2. **The SOP**: the step-by-step procedure from trip planning to approval, and the entry rules.
3. **Blank templates**: the Travel and Overhead tracker spreadsheets, a trip plan, and an approval-request email.

**Try it:** <https://jayceparabellum.github.io/trip-voucher-helper/>

## What's in the repo

| Path | What it is |
|---|---|
| [`index.html`](index.html) | The Trip Voucher Helper app. One self-contained page with no build step. |
| [`docs/SOP.md`](docs/SOP.md) | **TTP/SOP:** the 13-stage trip expense procedure (plan, approve, book, track, collect, PNG, file, enter, summary, PDF, attach, submit, review), with who does what, the gates, and the pitfalls. |
| [`docs/Expense-Report-Rules.md`](docs/Expense-Report-Rules.md) | A quick reference for the entry rules: taxes, lodging, M&IE, receipts, the PDF, comments, approvals. |
| [`templates/Travel_Expense_Tracker_Template.xlsx`](templates/Travel_Expense_Tracker_Template.xlsx) | Blank **Travel tracker** (Google Sheets workbook). Tabs: How to Use, Expenses, Mileage, Trips, Summary, Settings. |
| [`templates/Overhead_Expense_Tracker_Template.xlsx`](templates/Overhead_Expense_Tracker_Template.xlsx) | Blank **Overhead tracker** for training, certifications, drug tests, supplies, tools and PPE. Tabs: How to Use, Purchases, Summary, Settings. |
| [`docs/templates/trip-plan-template.md`](docs/templates/trip-plan-template.md) | Trip plan: site, GSA rates, max allowable, flight and hotel options, approvals. |
| [`docs/templates/approval-request-above-market-airfare.md`](docs/templates/approval-request-above-market-airfare.md) | Email template for above-market airfare, with variants for over-per-diem lodging and tool purchases. |

## The app

- **Ask questions** about the voucher process: tax placement, hotels, M&IE, parking, above-market fares, which receipt counts, comments, the PDF, and picking up where you left off.
- **Drop every receipt** (phone photos as JPEG or HEIC, screenshots, PDFs). Each one is converted once to a lossless PNG. PDF pages are rendered at 200 DPI. Blurry photos are flagged.
- **Review** every expense line in date order, with the GSA per diem days filled in and a note on how to enter each line in Unanet.
- **Build one PDF**: the trip timeline summary first (or your own Unanet summary screenshot), then one receipt per page in the same order, with nothing added to the receipt pages. It is named `<First initial>. <Last name> <report#>.pdf`.
- **Keep two trackers up to date**: the Travel tracker (flights, hotel, parking, rides, fuel, M&IE days) and the Overhead tracker (tools, material, training, PPE). Each expense type goes to the right one.

The tabs follow the work: **Trip → Receipts → Review → Packet**.

### Trackers: pick up where you left off

1. **First trip:** fill in the trip and receipts, then press **Save updated trackers** and **Save receipt PNGs** on the Packet tab. The app starts from the blank workbooks in [`templates/`](templates/). Upload each .xlsx to Google Drive and open it with Google Sheets.
2. **Next time:** in Google Sheets use File → Download → Microsoft Excel (.xlsx) for each tracker. Drop both files and the receipts .zip into the app, then pick the trip (or start a new one). Items, nights and rates come back, and the receipt images re-attach by file name.
3. **Put them back:** open the tracker in Google Sheets, then File → Import → Upload, pick the saved file and choose **Replace spreadsheet**.

The app writes only this trip's typed columns (date, vendor, amount, status and so on). Formulas, dropdowns, formatting and other trips' rows are left as they are. The sheet recalculates Event IDs, amounts owed, checks and summaries. App-only details (nights, nightly rate, parking days, receipt file names) go in a hidden `_voucher_app` sheet. This was tested with a real Google Sheets import and export: every formula and dropdown survived.

The app can't upload receipt images to Google Drive. Paste each Drive link into the tracker's Receipt link column yourself. The Overhead tracker shows "Missing receipt" until you do.

### What the trackers check

- **Travel tracker:** receipt needed (at or above the threshold on Settings, and always for lodging), possible duplicates, dates outside the trip, missing required fields, and meals over the GSA M&IE rate (75% on the first and last day unless the row is marked a continuous-travel full day). The Trips tab totals what you spent, what you're owed, what's been reimbursed, and the max M&IE. Mileage uses the IRS rate table on Settings.
- **Overhead tracker:** subtotal + sales tax + other fees, whether tax is split on Unanet (by category), the Unanet project and expense type, receipt check, duplicates, required fields, and totals by Unanet report number.
- **Settings tabs** hold the dropdown lists: travelers, categories, payment methods (and whether each is owed back to you), statuses, Unanet projects and expense types. Edit them for your own setup.

## Rules built in

| Item | Rule |
|---|---|
| M&IE | GSA rate. **75% only on the first day (home to the first site) and the last day (last site to home).** Every other day is full. A site-to-site travel day is claimed once, on the new trip, at 100% of the new site's rate. No receipt. |
| Lodging | Folio nightly rate, capped at the GSA lodging rate. All room taxes and fees go in the Tax box. |
| Parking | (daily cost + tax) × days, on one line |
| Airfare | One line at the total fare, taxes included |
| Separate tax line | Only for material, power tools, printing & copying, or equipment |
| Comments | Left empty |
| Receipts | Real photos or screenshots only, never transcriptions |
| Images | PNG only (lossless). The PDF embeds them losslessly. |
| Submitting | Never automatic. You review and submit in Unanet yourself. |

All the rules are in [`docs/Expense-Report-Rules.md`](docs/Expense-Report-Rules.md).

## Running it

- **Standalone** (open `index.html`, or use the GitHub Pages link above): everything except the Claude features works. The chat answers from the built-in process guide, and you fill in each receipt card yourself.
- **As a Claude artifact:** chat answers and "Read receipts with Claude" use the viewer's own Claude account, and saving goes through Claude's download prompt. The hosted copy carries the blank tracker templates inside the page.

## Privacy

- Receipts and trackers stay in your browser tab. They go to Claude only when you press "Read receipts", and only so Claude can fill in vendor, date and amount. Closing the tab clears them, so save first.
- The app never submits a report, sends email, or asks for card numbers or passwords.
- **This repo holds no one's real trips or spending.** The templates are blank, and the docs use placeholders. Keep your filled-in trackers, receipts, trip plans and emails in your own Drive and trip folders, never in this repo.

## Technical notes

- No build step and no server. Libraries load from public CDNs when needed: pdf.js 3.11.174, pdf-lib 1.17.1, JSZip 3.10.1, heic2any 0.0.4.
- Trackers are read and written with JSZip and the browser's XML parser, editing the workbook XML in place, with no spreadsheet library. Formula cells are never written.
- Blur check: variance of the Laplacian on a 640 px-wide copy. Photos are capped at about 9 MP. Summary pages are drawn at Letter size, 150 DPI.
