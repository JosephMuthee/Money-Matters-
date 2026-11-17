# THEE onset Enterprise — Version 5.0

A luxury-themed, mobile-first personal and multi-business finance command centre for Kenya. Default currency: KES. Includes M-Pesa recordkeeping and CSV statement import, budgets, savings goals, assets, debts, projects, investments, recurring transactions, monthly reports, audit trail, local backups, and optional Google Sheets sync.

## V5 additions

- **PIN or device biometric unlock:** retain the 4–8 digit PIN and optionally register a WebAuthn platform authenticator. On supported Android devices/browsers this can prompt for fingerprint, face, or device screen-lock verification. Android/browser support varies; use HTTPS (GitHub Pages is HTTPS). The browser never receives fingerprint images or biometric templates.
- **V4 data migration:** V5 imports existing V4/V3/V2/V1 local browser records on first launch.
- **GitHub Pages PWA:** install from Chrome on Android using Install app / Add to Home screen.
- **Google Sheets backend:** V4-compatible Apps Script and workbook included; backend supports transaction/account/asset/debt/repayment/project/investment/goal/recurring/business/settings/audit/sync/monthly report tabs.
- **Capacitor scaffold:** included for generating a native Android project locally; this ZIP is not a signed APK.

## Deploy to GitHub Pages

1. Extract this ZIP.
2. Create a GitHub repository, e.g. `thee-onset-enterprise`.
3. Upload the **contents** of this folder into the repository root (not the parent folder).
4. Open repository **Settings → Pages**; choose **Deploy from a branch**, branch `main`, folder `/ (root)`, then Save.
5. Wait for GitHub Pages to publish. URL format: `https://YOUR-USERNAME.github.io/thee-onset-enterprise/`.
6. Open the URL in Chrome on Android. Use **Install app** or Chrome menu → **Install app / Add to Home screen**.
7. In Settings, set a PIN and, if supported, select **Enable fingerprint**. The device may offer fingerprint, face, or screen-lock authentication.

## Google Sheets backend

1. Create a blank Google Sheet named **THEE onset Enterprise Backend**.
2. In the sheet, open **Extensions → Apps Script**. Replace the editor contents with the included `Code.gs`.
3. Replace `API_KEY` with a long, unique random key. Do not commit a real key to a public GitHub repository.
4. Save and run `setup` once; approve permissions. The script creates the required tabs.
5. Choose **Deploy → New deployment → Web app**; execute as **Me** and choose access that allows your own device to reach the endpoint. Deploy and authorize.
6. Copy the `/exec` URL. In the app, open **Settings & data**, paste the URL and same key, save, then choose **Sync now**.
7. The backend uses revision conflict checks; if another device saved since your last load, reload the cloud copy and reconcile changes before retrying. It does not automatically merge concurrent edits.

## Build a native Android APK

Requirements: Node.js LTS, Android Studio, Android SDK, and a Java version supported by the installed Android Gradle Plugin.

1. Extract the ZIP and open a terminal in the extracted folder.
2. Run `npm install`.
3. Run `npx cap add android` (once only).
4. Run `npx cap sync android`.
5. Run `npx cap open android` and allow Gradle sync to complete.
6. Test on a physical Android device/emulator.
7. For a test APK, use **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
8. For a distributable signed APK, use **Build → Generate Signed Bundle / APK** and create/protect your own signing key. Never share the keystore or passwords.

The package contains a Capacitor scaffold, not an already-built APK. WebAuthn biometric/device verification is for the HTTPS PWA/browser context; a fully native APK should integrate Android BiometricPrompt and be device-tested before relying on native biometrics.

## Security and recordkeeping

- Local records are stored in browser/WebView storage. Export backups regularly and sync to Google Sheets for a cloud copy.
- PIN hashing and WebAuthn platform authentication provide a local convenience lock, not encryption or a substitute for device security. The local client-side biometric check is not server-verified authentication and can be bypassed by someone able to modify the app or its local storage. Use Android screen lock and device encryption.
- WebAuthn may offer fingerprint, face, or device PIN depending on the Android device and browser. Fingerprint support is not guaranteed on every phone/browser.
- The Apps Script API key is a shared secret used by the client app. Anyone who obtains both the deployed endpoint and key may access the sheet. For production use, add authenticated server-side access control; do not expose secrets in public source code.
- Never store bank passwords, M-Pesa PINs, CVVs, one-time codes or authentication secrets in the app.
- M-Pesa manual recording and CSV import are included. Automatic live retrieval is not enabled; that requires Safaricom Daraja credentials, an approved use case, secure server-side integration and callback validation.
- Financial reports are management records based on entered data, not audited accounts, KRA filings or financial advice. Verify totals against official statements.

## Included workbook tabs

Transactions, Accounts, Assets, Debts, Debt Repayments, Projects, Investments, Goals, Recurring Transactions, Audit Log, Businesses, Settings, Sync Log, and Monthly Reports.
