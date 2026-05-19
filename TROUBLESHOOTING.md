# KIKI — Troubleshooting

## `npm` is not recognized (PowerShell)

**Cause:** Node.js is not installed, or it is not on your system `PATH`.

**Fix:**

1. Install **Node.js LTS** (20.x or 22.x): https://nodejs.org/
2. During setup, enable **“Add to PATH”**.
3. **Close and reopen** Cursor (and all terminals).
4. Verify:

   ```powershell
   node -v
   npm -v
   ```

5. From the project folder:

   ```powershell
   cd C:\Users\ulfea001\.cursor\projects\empty-window
   npm install
   npm run dev
   ```

## `ERR_CONNECTION_REFUSED` on http://localhost:3000

**Cause:** The dev server is not running.

**Fix:** Run `npm run dev` in the project folder and keep that terminal open. Use the URL printed in the terminal (often `http://localhost:3000`).

## `ERESOLVE` / peer dependency conflicts

This project includes a `.npmrc` with `legacy-peer-deps=true`. If install still fails:

```powershell
npm install --legacy-peer-deps
```

## Corporate proxy / SSL errors

If you see `UNABLE_TO_VERIFY_LEAF_SIGNATURE` or `ECONNRESET`, ask IT for proxy settings or try:

```powershell
npm config set strict-ssl false
```

(Only on trusted networks.)

## Still stuck?

Paste the **last 20 lines** of your terminal output after `npm install` or `npm run dev`.
