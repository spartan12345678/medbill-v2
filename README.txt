MEDBILL v2.0 - DEVELOPMENT BUILD

This is an offline-first browser/PWA prototype for pharmacy billing. It is not yet approved for commercial use or GST compliance.

IMPORTANT DATA PRESERVATION
- v2 opens the existing IndexedDB database named "medbill-local-v1" at database version 2.
- Existing v1 batches, invoices and shop settings are preserved by the additive database upgrade.
- Do not clear Chrome site data/storage.
- Export a v1 backup before upgrading as an additional precaution.
- GitHub Pages hosts public source files. Never upload transaction backups, GST certificates, customer data, passwords or API keys to the repository.

DEPLOYMENT
1. Upload the contents of this folder (index.html, app.js, styles.css, manifest.webmanifest, sw.js) to a separate GitHub repository or a v2-development branch.
2. Serve over HTTPS. GitHub Pages is supported.
3. Open the deployed URL in Chrome on Android.
4. Test using dummy data only.

V2 CHANGES
- Keeps the v1 IndexedDB database and adds movements/meta stores without deleting v1 data.
- Tax-inclusive pricing is the default for retail selling prices; exclusive pricing is also selectable.
- Intra-state tax is split into CGST plus UTGST when the shop state is Jammu and Kashmir; other intra-state supplies use CGST plus SGST. Inter-state supplies use IGST.
- GST invoice creation blocks if GSTIN, state, item GST rate or HSN is missing/invalid.
- Invoice serial length is checked against 16 characters; prefix and FY settings are configurable.
- Batch/expiry/HSN shown on invoice.
- Stock deduction and invoice creation use a single IndexedDB read/write transaction.
- Backup export and restore included.

KNOWN LIMITATIONS
- State/place-of-supply and tax-rate determinations need professional validation.
- HSN and GST rate lookup is manual; no live GST database integration.
- No e-invoice, e-way bill, GST return filing, credit-note workflow, sales returns, supplier purchase module, user roles, encryption, cloud sync or multi-device sync.
- Backup JSON is not encrypted. Store it securely.
- Browser/PWA local storage is not a substitute for a managed, backed-up production database.
- Verify all applicable CGST/UTGST/IGST provisions, Rule 46 invoice particulars, Rule 35 inclusive-tax computation, drug licence details, pharmacy recordkeeping and data-protection obligations before live use.

TESTING
Open browser developer console and run:
MedBillMath.splitTax(10,5,'inclusive',true)
Expected: taxable 9.52, tax 0.48, total 10.00 (rounded to paise).
MedBillMath.taxParts(0.48,true)
Expected: CGST 0.24, stateTax 0.24, IGST 0.
MedBillMath.invoiceNumber('GACRJK','2627',3)
Expected: GACRJK/2627/0003 (16 characters).
