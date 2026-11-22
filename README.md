# RPD Hub — RPD Management System

**Current prototype build: 0.4.7**  
**Deployment type: Static web app / local-browser prototype**

## Important data and security notice

This build is still a prototype. It stores records in the browser's `localStorage` on the current browser/device. Supabase is not connected, records do not sync between users/devices, and the role selector is a prototype preview rather than secure authentication or authorization.

Do not enter real resident personal information, diagnosis/medical information, or live financial records until the production database, authentication, authorization policies, backups, and security controls have been implemented and tested.

**Do not clear browser data or change the storage key when deploying an update if existing prototype test records must be retained.** The current storage key is `rpd_bookkeeping_v2`. Build 0.4.7 retains this key.

## Included files

- `index.html` — app interface and prototype logic
- `service-worker.js` — offline cache; cache version is `rpd-hub-047`
- `manifest.json` — PWA metadata
- `icon.svg`, `icon-192.png`, `icon-512.png` — app icons
- `rpd-logo-approved.jpeg` — approved RPD Hub logo
- `BUILD_0.4.4_NOTES.txt`, `BUILD_0.4.5_NOTES.txt`, `BUILD_0.4.6_NOTES.txt`, `BUILD_0.4.7_NOTES.txt` — historical build notes
- `CHANGELOG.md` — release history
- `TESTING.md` — test plan and current known test status
- `SPECIFICATION.md` — current prototype behaviour and known limitations

## Deploy / update

1. Keep a backup of the current deployed files and export a full JSON backup from Settings before changing the deployment.
2. Upload the contents of this folder to the existing GitHub Pages repository (not the enclosing ZIP folder).
3. Keep the existing browser/device and do not clear site data.
4. The service worker cache name is bumped for Build 0.4.7 so the browser can install the updated app files.
5. After deployment, reload the app. If an old screen remains, close/reopen the site or refresh once more; do not clear site data as a first troubleshooting step.
6. Verify the displayed build label is `BUILD 0.4.7 · PROTOTYPE`.

## Refund workflow in Build 0.4.7

- Discharging an admission calculates the refund using the existing 30-day rule.
- A refund marked pending is stored on the admission and is excluded from Cashbook totals.
- Admission Details now displays discharge/refund details.
- Owner can inspect the saved refund fields using the read-only **Inspect Saved Refund Data** diagnostic.
- Owner can record a pending refund payment later. The actual payment date and method are captured, and one linked posted Cash Out transaction is created.
- Duplicate linked refund transactions are blocked by the prototype logic.

## Known limitations

- Browser-local storage only; no cloud sync or multi-user persistence.
- Prototype role selector is not a security boundary.
- No production authentication, authorization, Supabase schema, secure document storage, or server-side audit controls are provided by this ZIP.
- Browser storage can be lost if site data is cleared or the browser/device is changed. Export backups regularly.


BUILD 0.4.9 ASSET NOTE
- `rpd-logo-approved.jpeg`, `icon-192.png`, and `icon-512.png` are the approved RPD Hub app icon assets.
- `rpd-letterhead-logo.png` is the separate official Rumah Penjagaan Damai letterhead logo used in Reports preview, PDF, and Print.
