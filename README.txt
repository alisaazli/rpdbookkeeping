RPD BOOKKEEPING — DEVELOPMENT BUILD 0.2
Rumah Penjagaan Damai

WHAT IS INCLUDED IN THIS BUILD
- Graphite & Electric Violet visual identity, Light/Dark theme
- Responsive iPhone-first layout; supports iPad, Android tablets and desktop widths
- Dashboard with month selector, opening bank balance, Cash In, Cash Out and closing balance
- Monthly cash-flow chart and annual overview
- 21 original Cash Out categories and subcategories, plus editable Cash In categories
- Dynamic category/subcategory suggestions and rule-based learning memory
- Learning Rules page to edit/delete learned phrases
- Category required before a transaction can be saved; unresolved suggestion is shown as PERLU SEMAK
- Owner direct posting; Admin/Staff submissions marked pending in the local prototype
- Owner approval queue for pending submissions
- Admin edit proposal workflow in the local prototype (original record remains unchanged pending approval)
- Owner drafts; drafts excluded from financial totals
- Transaction history with search, month/type/category filters and monthly totals
- Soft-delete Trash and Restore
- Receipt upload (multiple files), original file preservation and in-browser OCR text extraction for image files
- Receipt preview and original download; basic image-to-PDF copy option
- Reports with custom date range, category breakdown, CSV, PDF and print
- Monthly opening bank balance override and carry-forward calculation
- JSON backup and restore
- Append-only activity history in the local prototype
- Supabase starter schema in supabase/schema.sql

IMPORTANT — CURRENT STORAGE / SECURITY STATUS
This is a front-end development prototype. It currently stores data in localStorage in the browser/device.
It is NOT yet connected to Supabase, does NOT provide real multi-user sync, and does NOT provide production authentication or server-enforced permissions.
The role selector in Settings is only a UI workflow preview. It is not a security control. Do not use this build as the live source of official RPD financial records yet.

SUPABASE NEXT STEPS
1. Create the RPD Supabase project.
2. Review and run supabase/schema.sql in Supabase SQL Editor.
3. Create the first Owner account and securely assign the owner role to its profile (the initial Owner bootstrap must be performed by a trusted project administrator).
4. Verify every Row Level Security policy with separate Owner, Admin, Staff and Viewer test accounts.
5. Configure private receipt storage, database backup, restore tests and retention before importing real financial data.
6. Integrate Supabase Auth, database queries and Storage into the frontend. Do not put a service-role key in index.html. Only the anon/publishable key may be used in a browser, with correct RLS.
7. Configure a scheduled backup/export strategy that genuinely meets the 365-day retention target. Supabase plan defaults alone should not be assumed to provide this.

RUN LOCALLY
- Extract the ZIP.
- Run: python -m http.server 8000
- Open: http://localhost:8000
- For PWA installation, deploy to HTTPS (e.g. GitHub Pages) and open the site in Safari/Chrome.

DEPLOY TO EXISTING GITHUB PAGES
Upload/replace the contents of this folder in the repository root, keeping the folder structure (index.html, manifest.json, service-worker.js, icon.svg, supabase/schema.sql).
The existing site URL remains the same if the repository and Pages settings are unchanged.

OCR AND RECEIPT LIMITATIONS IN THIS BUILD
OCR extracts text from selected image receipts in the browser and displays the extracted text for review. It does not yet reliably identify and pre-fill receipt date, merchant and total amount as separate verified fields. PDF receipts are stored/downloadable but OCR is not run on PDF files in this build. The PDF copy is a basic image-to-PDF output, not a full edge-detection/perspective-correction scanner. These are follow-on implementation tasks before production.

DATA MIGRATION
The new prototype uses a new localStorage key (rpd_bookkeeping_v2), so it does not automatically import the old v1 browser data. Keep the previous version and its JSON backup. Before migrating existing records, export a backup from the old app and perform a controlled migration test. Do not delete the old app data until verified.

COST / COMPLIANCE
No current Supabase plan or price is assumed. Verify database, storage, bandwidth, backup and restore costs before production. The currently selected five-year receipt retention period should be checked with the RPD accountant/tax adviser before it is treated as final compliance policy.
