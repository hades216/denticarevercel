# Troubleshooting Guide

## Build Issues

### Error: "Cannot find module '@tanstack/react-start'"
**Cause:** Old dependencies still installed
**Solution:**
```bash
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Error: "vite: command not found"
**Cause:** Dependencies not installed
**Solution:**
```bash
npm install
```

### Build succeeds but dist folder is empty
**Cause:** Build output directory issue
**Solution:**
1. Delete `dist` folder
2. Run `npm run build` again
3. Check that `dist/index.html` exists

---

## Deployment Issues

### Can't connect to IONOS FTP
**Cause:** Wrong credentials or server address
**Solution:**
1. Check IONOS control panel for FTP details
2. Verify username and password
3. Try different FTP port (21 or 22)
4. Contact IONOS support if still failing

### Files uploaded but .htaccess missing
**Cause:** FTP client hiding hidden files
**Solution:**
1. In FileZilla: View → Show hidden files
2. In WinSCP: View → Show hidden files
3. Re-upload `.htaccess` from `public/` folder
4. Verify it appears in root directory

### Upload takes too long
**Cause:** Large files or slow connection
**Solution:**
1. Use SFTP instead of FTP (faster)
2. Upload during off-peak hours
3. Check internet connection speed
4. Try uploading in smaller batches

---

## Runtime Issues

### Pages show 404 errors
**Cause:** `.htaccess` not working or not uploaded
**Solution:**
1. Verify `.htaccess` exists in root directory
2. Check file permissions (should be 644)
3. Enable "Show hidden files" in FTP and verify upload
4. Contact IONOS to enable `mod_rewrite` module

**Test if .htaccess is working:**
- Try accessing `/about` directly
- If you get 404, `.htaccess` isn't working
- If page loads, `.htaccess` is working

### Styles and images not loading
**Cause:** Asset paths incorrect or files not uploaded
**Solution:**
1. Clear browser cache (Ctrl+Shift+Delete)
2. Hard refresh (Ctrl+F5)
3. Check browser console (F12) for 404 errors
4. Verify all files in `dist/assets/` were uploaded
5. Check file permissions (should be 644)

### Site loads but navigation doesn't work
**Cause:** Client-side routing not configured
**Solution:**
1. Check `.htaccess` is in root directory
2. Verify `.htaccess` has correct permissions (644)
3. Check that `RewriteEngine On` is in `.htaccess`
4. Contact IONOS if `mod_rewrite` is disabled

### Blank page or white screen
**Cause:** JavaScript error or React not loading
**Solution:**
1. Open browser console (F12)
2. Check for JavaScript errors
3. Check Network tab for failed requests
4. Verify `index.html` was uploaded
5. Check that `src/main.tsx` is referenced in `index.html`

### Images show broken links
**Cause:** Image paths incorrect
**Solution:**
1. Check image files exist in `dist/assets/`
2. Verify image paths in HTML (should be relative)
3. Check file permissions (644)
4. Clear browser cache

---

## Performance Issues

### Site loads slowly
**Cause:** Large assets or no compression
**Solution:**
1. Verify `.htaccess` compression is enabled
2. Check browser Network tab for large files
3. Optimize images locally before build
4. Enable browser caching (check `.htaccess`)

### JavaScript files are large
**Cause:** Code not minified
**Solution:**
1. Verify build is in production mode
2. Check `vite.config.ts` has `minify: "terser"`
3. Run `npm run build` again
4. Check `dist/assets/` for minified files

---

## Supabase Integration Issues

### Supabase calls fail
**Cause:** Environment variables not set
**Solution:**
1. Create `.env` file locally with:
   ```
   VITE_SUPABASE_URL=your_url
   VITE_SUPABASE_ANON_KEY=your_key
   ```
2. Run `npm run build` to embed variables
3. Re-upload `dist/` folder
4. Verify variables are in `dist/assets/main.*.js`

### CORS errors from Supabase
**Cause:** Domain not allowed in Supabase
**Solution:**
1. Go to Supabase project settings
2. Add your IONOS domain to allowed origins
3. Include protocol (https://yourdomain.com)
4. Wait a few minutes for changes to propagate

---

## Browser-Specific Issues

### Works in Chrome but not Firefox
**Cause:** Browser cache or compatibility issue
**Solution:**
1. Clear Firefox cache
2. Check browser console for errors
3. Try incognito/private mode
4. Update browser to latest version

### Mobile site looks broken
**Cause:** Responsive design issue
**Solution:**
1. Check viewport meta tag in `index.html`
2. Test with browser DevTools mobile view
3. Verify CSS media queries are working
4. Check that Tailwind CSS is loaded

---

## File Permission Issues

### Can't access files after upload
**Cause:** Wrong file permissions
**Solution:**
1. Set file permissions to 644
2. Set directory permissions to 755
3. Set `.htaccess` permissions to 644
4. Most FTP clients do this automatically

**In FileZilla:**
1. Right-click file → File permissions
2. Set to 644 (or 755 for directories)

**In WinSCP:**
1. Right-click file → Properties
2. Set permissions accordingly

---

## Debugging Steps

### General troubleshooting process:
1. **Check browser console** (F12 → Console tab)
   - Look for JavaScript errors
   - Check for failed network requests

2. **Check Network tab** (F12 → Network tab)
   - Verify all files load (no 404s)
   - Check response status codes
   - Look for failed requests

3. **Check file uploads**
   - Verify all files in `dist/` were uploaded
   - Check `.htaccess` is in root
   - Verify file permissions

4. **Test locally first**
   - Run `npm run dev`
   - Test all pages work
   - Check console for errors

5. **Clear cache**
   - Browser cache (Ctrl+Shift+Delete)
   - Hard refresh (Ctrl+F5)
   - Try incognito mode

6. **Contact support**
   - IONOS support for hosting issues
   - Check IONOS documentation
   - Provide error messages and steps to reproduce

---

## Getting Help

### Before contacting support, provide:
- Error message (exact text)
- Steps to reproduce
- Browser and version
- Screenshot of issue
- Console errors (F12)

### Useful resources:
- IONOS Help: https://www.ionos.com/help
- Browser DevTools: F12
- Network tab: F12 → Network
- Console: F12 → Console

### Common IONOS settings:
- FTP Server: Check IONOS control panel
- Root directory: Usually `public_html` or `www`
- Modules: Check if `mod_rewrite` is enabled
- PHP version: Not needed for static sites
