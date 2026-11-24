# Trip Expense SOP (Tactics, Techniques and Procedures)

How a field technician takes a work trip from assignment to a submitted expense report (voucher) in Unanet. It has 13 stages in 3 phases. The **Trip Voucher Helper** app does stages 4 through 7, 9 and 10 for you. The rules in [Expense-Report-Rules.md](Expense-Report-Rules.md) apply at every stage.

**Who does what**

| Tag | Meaning |
|---|---|
| **You** | A manual step or a decision only you make |
| **App** | The Trip Voucher Helper (or an assistant) does it |
| **System** | Where the data lives: Unanet, Google Sheets, Google Drive, email |
| **Gate** | A rule that must pass before the next stage |

```
1 Plan → 2 Approve → 3 Book → 4 Track → 5 Collect → 6 PNG → 7 File
→ 8 Enter → 9 Summary → 10 PDF → 11 Attach → 12 Submit → 13 Review
```

---

## Phase 1: Before the trip (stages 1–4)

### 1. Plan the trip
- **Inputs:** job site, dates, travel days; the GSA per diem for the locality ([gsa.gov](https://www.gsa.gov/travel/plan-book/per-diem-rates), by ZIP and month); flight and hotel searches.
- **Work:**
  - Look up the lodging cap and the M&IE rate (full day, plus 75% for the first and last travel days).
  - Shortlist nonstop flights and note the bag fees.
  - Shortlist hotels **with a kitchen**, at or under the lodging cap. Never a resort.
  - Work out the max allowable: lodging (nights × cap) + M&IE (see the M&IE rules).
- **Outputs:** a trip folder named `YYYY-MM_City-ST`, and a trip plan from [templates/trip-plan-template.md](templates/trip-plan-template.md).

### 2. Get approval when needed
- **When:** a fare is above market or over per diem (holiday travel, last-minute changes); any purchase of material, tools or equipment; a card or travel-form exception.
- **Work:** draft the request with the evidence attached as PNG (the receipt, the quote, or a screenshot of comparable fares). Use [templates/approval-request-above-market-airfare.md](templates/approval-request-above-market-airfare.md).
- **Gate:** you review and send every email yourself. Keep the written approval with the trip.

### 3. Book
- **You** book and pay. An assistant never enters card numbers or passwords.
- Lodging at or under per diem. Never a resort.
- **Outputs:** confirmation emails; confirmation numbers in your trip plan, which stays on your own machine.

### 4. Open the trackers *(App)*
- **Inputs:** trip dates, site ZIP, GSA rates, bookings.
- **Work:**
  - Add the trip row (`T-00N`) on the Travel tracker's **Trips** tab, with the site ZIP and GSA rates.
  - Add expense rows. Event IDs (`T-00N-NN` travel, `T-00N-SNN` overhead) are numbered by the sheet.
  - Add one M&IE row per day.
  - Make the trip's Drive receipts folder.
- **Outputs:** the Travel tracker (Trips + Expenses) and, for purchases, the Overhead tracker (Purchases). Expected flags at this point: "Receipt needed" and "Outside trip dates" (for airfare bought ahead).
- **In the app:** fill in the Trip tab, then **Save updated trackers**. First time: upload the .xlsx files to Drive and open them with Google Sheets.

---

## Phase 2: During and after the trip (stages 5–7)

### 5. Collect receipts
- **Inputs:** emailed receipts (airline, rideshare, training, online orders), vendor PDFs (hotel folio), phone photos (parking ticket, fuel).
- **Work:** find the **real** receipt, not a look-alike:
  - **Rideshare:** the trip receipt ("Thanks for riding"), not the charge summary.
  - **Amazon:** the Order Summary print page that lists every item and price, not the "thanks for your order" email.
  - **Hotel:** the final folio from checkout, not the reservation.
- **Output:** one source document per expense.

### 6. Capture each receipt as PNG *(App)*
- **Work:**
  - Email: a screenshot of the original email.
  - PDF: rendered at 200 DPI.
  - Phone JPEG or HEIC: converted to PNG **once**, then only the PNG is used.
  - Long web page: zoomed capture, stitched.
- **Gate:**
  - Real photos or screenshots only, never typed transcriptions.
  - **PNG only, no JPEG.**
  - Clear and readable. Retake anything blurry; the app flags soft photos.
- **In the app:** drop every file in the chat or on the Receipts tab.

### 7. File and link
- Save each PNG in the trip folder and upload it to the trip's Drive receipts folder: one file per receipt, no duplicates.
- Put each file's Drive link in the tracker's **Receipt link** column. The app can't upload to Drive, so you paste the link.
- **In the app:** **Save receipt PNGs (.zip)** gives you the files, already named and in timeline order.

---

## Phase 3: The expense report (stages 8–13)

### 8. Enter lines in Unanet
- One line per expense, following the [entry rules](Expense-Report-Rules.md). The app's **Review** tab lists each line in date order with "How to enter".
- **Lodging:** use the per diem wizard. The GSA rate is the allowance and the folio rate is the daily rate. All taxes and fees go in the Tax box.
- **M&IE:** use the per diem wizard. No receipt.
- Leave **Comments** empty.
- **Gate:** save the report; don't submit yet. Write a comment only when your approver asks for specific text.

### 9. Capture the report summary
- Screenshot the saved Unanet report summary as PNG. Or let the app draw a trip timeline summary page.

### 10. Build the one PDF *(App)*
- Page 1 is the summary. After it comes one receipt per page in line order, with nothing added on the receipt pages.
- Images are embedded losslessly.
- Name: `<First initial>. <Last name> <report#>.pdf`, for example `J. Smith 12345.pdf`.

### 11. Attach and distribute
- Attach the PDF as the report's **only** attachment, then save.
- Check that the stored file size matches.
- Copy the same PDF, with the same name, to the trip folder and the trip's Drive folder.

### 12. Review and submit
- **You** check totals, lines and receipts, then click **Submit**.

### 13. Approval and corrections
- Your approver reviews and may correct lines. Turn any new guidance into a written rule and add it to [Expense-Report-Rules.md](Expense-Report-Rules.md).
- **Pitfall:** never click **Edit** (the pencil) on a report that is in approval. It pulls the report back to "In Use", and it has to be resubmitted. Ask for the changes by email instead.
- **In the app:** **Save updated trackers**, then mark the status (Submitted, Reimbursed) as it changes.

---

## Systems in the loop

| System | Role |
|---|---|
| Email | Where vendor receipts arrive; approvals and approver feedback |
| Google Sheets | Travel and Overhead trackers: trips, expenses, receipt links, totals owed |
| Google Drive | Per-trip receipt folders and report PDFs |
| Trip folder (your computer) | Working copies and the trip plan |
| Unanet | System of record: submission and approval |
| gsa.gov | Per diem rates by locality and month |
| Trip Voucher Helper | Receipts to PNG, line review, the PDF, tracker updates |

## Where an assistant must stop
- It never submits a report, sends email, or enters a card number or password.
- It never writes Unanet comments unless you give the exact text.
- It drafts. You review and act.
