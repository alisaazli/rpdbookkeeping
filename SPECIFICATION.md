# RPD Hub — Prototype Specification (Build 0.4.7)

## 1. Product

- Product name: RPD Hub
- Formal system name: RPD Management System
- Organisation: Rumah Penjagaan Damai
- Build: 0.4.7
- Current delivery: static web/PWA prototype

## 2. Current storage and security boundary

- App records are stored in browser `localStorage`.
- Current key: `rpd_bookkeeping_v2`.
- Supabase is not connected in this build.
- Data does not sync across devices or users.
- The role selector is a local prototype preview and is not secure authentication or authorization.
- Do not use real resident or medical data in this prototype.

## 3. Current app areas

The source includes Dashboard, Add Transaction, Transaction History, Approvals, Drafts, Categories, Learning Rules, Reports, Trash, Audit Trail, Settings, Residents, and Admissions.

## 4. Cashbook and reports

- Posted Cash In and Cash Out transactions contribute to totals.
- Pending refunds are not posted Cash Out transactions and must not change Cashbook totals.
- A refund payment recorded later creates a posted Cash Out transaction dated on the actual payment date.
- Refund transactions use the `REFUND (DISCAJ)` category and link to the admission record.
- Existing report/export functions are retained from the supplied source.

## 5. Resident and admission records

- Resident profiles are stored separately from admission records.
- A resident may have multiple admission records.
- Admission records include admission date, monthly fee, deposit amount/status, and admission status.
- Deposit payment is recorded against an admission.
- An admission can be activated after the required deposit is paid.
- Active admissions can be discharged.
- Discharge status and history are retained in the resident's admission history.

## 6. Discharge refund calculation

The current prototype applies a 30-day calculation:
- Daily rate = monthly fee ÷ 30.
- Discharge day is capped between day 1 and day 30.
- If current month's fee is paid: gross refund = deposit + remaining days' fee.
- If current month's fee is unpaid: gross refund = deposit − occupied days' fee.
- Other deductions reduce the refund.
- Refund and amount still due are floored at zero.
- This is a prototype rule implementation and must be validated by the Owner before real-world use.

## 7. Refund lifecycle

### Pending at discharge
- Admission is marked discharged.
- Calculated refund amount, calculation breakdown, amount still due, refund status, and discharge details are saved on the admission.
- Status is `pending` when refund is greater than zero and was not paid at discharge.
- No Cashbook transaction is created for a pending refund.
- Audit event records the pending refund.

### Paid at discharge
- If marked paid during discharge and refund is greater than zero, the app creates a posted linked Cash Out transaction.
- Admission refund status is `paid`.

### Pay a previously pending refund
- Owner can open the discharged admission and select Record Refund Payment.
- The form captures actual payment date, method, optional reference, and notes.
- A linked posted Cash Out transaction is created under `REFUND (DISCAJ)`.
- Admission refund status changes from `pending` to `paid`.
- Payment details and transaction ID are saved on the admission.
- Audit event `DEPOSIT_REFUND_PAID` is written.
- The prototype blocks a duplicate linked system-generated refund transaction for the same admission.

## 8. Diagnostic

- Owner can select Inspect Saved Refund Data from a discharged admission.
- Diagnostic is read-only.
- It compares the in-memory admission record with the persisted record under `rpd_bookkeeping_v2`.
- It reports refund fields and related audit events without exporting unrelated resident profile details.
- It does not modify or reset storage.

## 9. Explicitly not production-ready

This ZIP does not implement production-grade:
- Authentication and server-side role enforcement.
- Supabase database connection, schema, RLS policies, or secure storage.
- Multi-user synchronization.
- Server-side immutable audit logging.
- Production backup/restore infrastructure.
- Secure handling of sensitive resident diagnosis and supported documents.

These remain separate implementation requirements and must not be represented as completed by this prototype.
