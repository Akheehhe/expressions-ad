# Expressions a.d — Site

Marketing site + admin license generator. Deploys free on GitHub Pages.

## Files

| File | Purpose |
|---|---|
| `index.html` | Public landing page (features, install, pricing) |
| `admin.html` | Password-protected license generator + history |
| `style.css`  | Shared styles |

## Deploy to GitHub Pages

1. Create a new GitHub repo, e.g. `expressions-ad`
2. Push these files to the `main` branch
3. Repo settings → **Pages** → Source: Deploy from branch → `main` / `(root)` → Save
4. Wait ~30 seconds. Site live at: `https://YOUR_USERNAME.github.io/expressions-ad/`
5. Admin panel: `https://YOUR_USERNAME.github.io/expressions-ad/admin.html`

### Quick deploy commands

```bash
cd C:/Users/TechSwap/claude/expressions-ad-site
git init
git add .
git commit -m "Initial deploy"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/expressions-ad.git
git push -u origin main
```

## Important: change the admin password

Open `admin.html`, find this line near the bottom:

```js
const ADMIN_PASS  = 'changeme123';
```

Change `'changeme123'` to your own password. Anyone who visits `admin.html` needs this to generate keys.

> ⚠️ The password is client-side only — anyone who views the source can see it. Use a long, random string. For real security, host the admin behind a server-side auth layer or keep the admin URL secret.

## Important: secret salt

The salt in `admin.html` MUST match the salt in the plugin's `js/main.js`:

```js
const SECRET_SALT = 'ExpressionsLib2026_xYz!!_SuperSecret_1a2b3c4d';
```

If you change one, change both — otherwise generated keys won't validate.

## Generating license keys

1. Visit `admin.html`
2. Enter the admin password
3. Fill: customer note, days/hours/minutes
4. Click **⚡ Generate Key**
5. Copy the green key, send to customer
6. History is stored in browser localStorage — won't sync between devices

## Sending key to customer

Customer pastes the key into the plugin's License Activation screen on first launch.
Plugin validates HMAC + expiry locally, no server call needed.
