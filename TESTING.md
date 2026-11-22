# RPD Hub — Testing Checklist

## Test environment

- Build: 0.4.7
- Storage: browser `localStorage`
- Storage key: `rpd_bookkeeping_v2` (intentionally unchanged)
- Supabase: not connected
- Use TEST RESIDENT and synthetic data only.

## Existing Test A — fee paid, refund pending

Original scenario:
- Resident: TEST RESIDENT
- Admission date: 21 Nov 2026
- Monthly fee: RM3,000
- Deposit: RM3,000, paid
- Discharge date: 22 Nov 2026
- Current month's fee paid: Yes
- Other deductions: RM0
- Refund paid to resident at discharge: No
- Expected refund: RM3,800 (RM3,000 deposit + RM800 remaining fee)
- Expected amount still due: RM0
- Expected refund status: Pending
- Expected Cashbook change at discharge: RM0

Observed in Build 0.4.6 from owner-provided screenshots:
- Calculation preview and confirmation: RM3,800.
- Admission changed to Discharged.
- Cashbook totals remained Cash In RM100, Cash Out RM41, Net RM59; latest visible transaction remained 17 Nov 2026.
- Resident Profile and Admission Details did not display refund amount/status.
- Whether the refund fields were persisted in browser storage was not yet independently verified.

### Build 0.4.7 verification steps

1. Deploy Build 0.4.7 without clearing site data.
2. Confirm the header shows Build 0.4.7.
3. Open Residents → TEST RESIDENT → View → View admission for 21 Nov 2026.
4. Confirm Admission Details displays:
   - Discharge date 22 Nov 2026
   - Refund amount RM3,800
   - Refund status Pending
   - Amount still due RM0
5. Tap **Inspect Saved Refund Data**.
6. Confirm:
   - `savedRecordFound` is true
   - `persistedFields.refundAmount` is 3800
   - `persistedFields.refundStatus` is `pending`
   - `persistedFields.amountStillDue` is 0
   - `linkedRefundCashbookTransaction` is false
   - a related `DEPOSIT_REFUND_PENDING` audit event exists
7. Recheck History. Cashbook totals must remain unchanged until the refund is actually paid.
8. Do not record payment during this verification step unless intentionally testing the payment workflow.

## Test A payment-completion subtest

Only after pending refund persistence is confirmed:
1. Open the same discharged admission.
2. Tap **Record Refund Payment**.
3. Enter the actual test payment date and method.
4. Confirm payment once.
5. Verify refund status changes to Paid.
6. Verify exactly one linked Cash Out transaction for RM3,800 appears on the selected payment date.
7. Verify audit event `DEPOSIT_REFUND_PAID` exists.
8. Reopen the admission and attempt to access payment action again; a duplicate transaction must not be created.

## Test B — fee unpaid

Create a separate new TEST RESIDENT admission with a new RM3,000 paid deposit. Do not reuse the discharged 21 Nov admission.

Scenario:
- Monthly fee: RM3,000
- Deposit: RM3,000, paid
- Discharge date: 22 Nov 2026
- Current month's fee paid: No
- Other deductions: RM0
- Refund paid at discharge: No
- Expected occupancy fee: 22 × RM100 = RM2,200
- Expected refund: RM800
- Expected amount still due: RM0
- Expected refund status: Pending
- Expected Cashbook change at discharge: RM0

## Regression checks

- Existing transactions and test records remain present after deployment.
- No browser storage reset occurs.
- Existing admissions remain in history.
- Pending refunds do not affect posted Cashbook totals or reports.
- A paid refund creates only one linked Cash Out transaction.
- Payment date is the actual payment date, not automatically the discharge date.

## Status discipline

Do not mark Test A fully passed until the persisted refund diagnostic and the pending Cashbook exclusion have both been verified on the live iPhone deployment. Test B remains blocked until Test A persistence is verified.
