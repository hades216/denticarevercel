# Quick Start - Deploy to IONOS

## 3-Step Deployment

### Step 1: Build
```bash
npm install
npm run build
```

### Step 2: Upload
1. Open FTP client (FileZilla, WinSCP, etc.)
2. Connect to IONOS FTP server
3. Upload everything from `dist` folder to `public_html`
4. **Make sure `.htaccess` is uploaded** (enable "Show hidden files")

### Step 3: Test
Visit your domain and test all pages work.

## What Changed

✅ Removed server-side dependencies (Cloudflare, Netlify plugins)
✅ Created static SPA build configuration
✅ Added `.htaccess` for SPA routing on IONOS
✅ Created `index.html` entry point
✅ Created `src/main.tsx` entry point
✅ Optimized for static hosting

## Key Files

- **`dist/`** - Your deployment folder (upload this to IONOS)
- **`public/.htaccess`** - Critical for routing (must be uploaded!)
- **`index.html`** - Entry point
- **`src/main.tsx`** - React app entry

## Important

⚠️ The `.htaccess` file is **hidden by default**. You must:
1. Enable "Show hidden files" in your FTP client
2. Upload it to the root of your hosting
3. Set permissions to 644

Without `.htaccess`, page routing won't work!

## Troubleshooting

**Pages show 404?**
- Check `.htaccess` is uploaded
- Enable `mod_rewrite` in IONOS control panel

**Styles/images missing?**
- Clear browser cache
- Verify all files uploaded
- Check file permissions

**Need help?**
- See `IONOS_DEPLOYMENT.md` for detailed guide
- See `DEPLOYMENT_CHECKLIST.md` for step-by-step checklist
