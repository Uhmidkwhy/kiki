# Put KIKI on GitHub

Your project folder:

`C:\Users\ulfea001\.cursor\projects\empty-window`

**Never upload:** `node_modules`, `.next`, `.env.local` (secrets).  
`.gitignore` already excludes these if you use Git.

---

## Step 1 — Create a GitHub account

1. Go to [https://github.com](https://github.com)
2. Sign up (free). Use a personal email you can access.

---

## Step 2 — Create an empty repository

1. Click **+** (top right) → **New repository**
2. Name it e.g. `kiki`
3. Leave it **Public** (or Private if you prefer)
4. **Do not** check “Add a README” (you already have files)
5. Click **Create repository**

GitHub shows a page with setup commands. Keep that tab open.

---

## Step 3 — Upload with Git (recommended if `git` works)

Open PowerShell in the project folder:

```powershell
cd C:\Users\ulfea001\.cursor\projects\empty-window
git --version
```

If you see a version number, continue:

```powershell
git init
git add .
git commit -m "Initial commit: KIKI chat app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/kiki.git
git push -u origin main
```

Replace `YOUR_USERNAME` and `kiki` with your repo URL from GitHub.

### First-time push login

GitHub no longer accepts account passwords in the terminal. Use a **Personal Access Token**:

1. GitHub → profile picture → **Settings**
2. **Developer settings** → **Personal access tokens** → **Tokens (classic)**
3. **Generate new token (classic)** → enable **repo**
4. Copy the token
5. When `git push` asks for a password, **paste the token** (not your GitHub password)

---

## Step 3 (alternate) — No Git installed

### A) GitHub Desktop

1. Install [GitHub Desktop](https://desktop.github.com) if your school allows it
2. **File → Add local repository** → choose `empty-window`
3. **Publish repository** to GitHub

### B) Upload in the browser

1. On the new repo page, click **uploading an existing file**
2. Drag in everything from `empty-window` **except**:
   - `node_modules` (folder)
   - `.next` (folder, if it exists)
   - `.env.local` (secrets)
3. Click **Commit changes**

---

## Step 4 — Confirm

Refresh `https://github.com/YOUR_USERNAME/kiki` — you should see `package.json`, `src/`, `README.md`, etc.

---

## Next: run without local Node

- **StackBlitz:** Import this GitHub repo at [stackblitz.com](https://stackblitz.com)
- **Vercel:** [vercel.com](https://vercel.com) → Import Project → select the repo → add `OPENAI_API_KEY` in Environment Variables → Deploy

---

## Checklist before you push

- [ ] No `.env.local` in the repo (only `.env.example`)
- [ ] No `node_modules` folder committed
- [ ] API keys only in Vercel/StackBlitz env settings, not in code
