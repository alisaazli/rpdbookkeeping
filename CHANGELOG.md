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
