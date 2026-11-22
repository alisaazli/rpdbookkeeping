# Changelog

## Build 0.4.7 — Refund visibility and payment completion

- Admission Details displays discharge date, current-month fee-paid selection, refund amount, refund status, amount still due, and refund payment details when present.
- Added a read-only Owner diagnostic that compares in-memory refund fields with the admission record persisted under the existing `rpd_bookkeeping_v2` localStorage key.
- Added Owner workflow to record a previously pending refund as paid.
- Captures actual refund payment date, method, optional reference, and notes.
- Creates one linked, posted Cash Out transaction under `REFUND (DISCAJ)` when a pending refund is paid.
- Blocks a second linked system-generated refund transaction for the same admission.
- Adds audit event `DEPOSIT_REFUND_PAID` for a later refund payment.
- Retains existing localStorage key to preserve current browser test data.
- Bumps service-worker cache to `rpd-hub-047`.

## Build 0.4.6

- Discharge asks whether the calculated refund has actually been paid.
- Paid refunds create a linked posted Cash Out transaction.
- Pending refunds are saved on the admission and do not affect Cashbook totals.
- Adds discharge/refund audit events.

## Build 0.4.5

- Modern SaaS visual refresh.
- Admissions summary by selected month.
- Report letterhead and improved print/PDF layout.
- Existing discharge refund rules retained.

## Build 0.4.4

- Resident Profile discharge action.
- 30-day discharge refund calculation.
- Expanded CSV, Excel, PDF, and print reporting.

## Build 0.4.8 — Reports and official letterhead correction

- Separated the exact RPD Hub app icon from the official letterhead logo.
- Reports preview, PDF and Print use the user-supplied official letterhead logo and only the approved company details.
- Fixed mobile Reports overflow caused by the letterhead image rendering at its natural dimensions.
- Improved iPhone report controls, metrics and transaction layout.
- PDF now repeats the official letterhead and transaction table headings across pages.
- Preserved the existing localStorage key and bumped the service-worker cache to `rpd-hub-048`.

## Build 0.4.9
- Corrected print stylesheet specificity so mobile transaction cards cannot leak into print output.
- Restored high-contrast tabular transaction layout, repeating column headers, and page-break-safe rows.
- Repeated official RPD letterhead on printed pages; retained the supplied approved logo files unchanged.
- Added thousands separators to PDF transaction amounts.
- Updated service-worker cache and PWA version; preserved application data key and workflows.
