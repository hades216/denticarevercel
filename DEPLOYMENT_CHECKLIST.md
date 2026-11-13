# IONOS Deployment Checklist

## Pre-Deployment

- [ ] All dependencies installed (`npm install` or `bun install`)
- [ ] Project builds successfully (`npm run build`)
- [ ] No console errors in development (`npm run dev`)
- [ ] All pages tested locally
- [ ] Environment variables configured (if needed)
- [ ] Images and assets are optimized

## Build & Prepare

- [ ] Run `npm run build` to create the `dist` folder
- [ ] Verify `dist` folder contains:
  - [ ] `index.html`
  - [ ] `assets` folder with JS and CSS files
  - [ ] All image files

## FTP Upload

- [ ] Connect to IONOS FTP server
- [ ] Navigate to `public_html` or `www` folder
- [ ] **Enable "Show hidden files"** in your FTP client
- [ ] Upload all files from `dist` folder
- [ ] **Verify `.htaccess` is uploaded** (critical!)
- [ ] Check file permissions:
  - [ ] Files: 644
  - [ ] Directories: 755
  - [ ] `.htaccess`: 644

## Post-Deployment

- [ ] Visit your domain in browser
- [ ] Test homepage loads
- [ ] Test navigation between pages
- [ ] Test all links work
- [ ] Check images load correctly
- [ ] Test on mobile device
- [ ] Check browser console for errors (F12)
- [ ] Verify styles are applied correctly

## Troubleshooting

If pages show 404:
- [ ] Verify `.htaccess` exists in root
- [ ] Check `.htaccess` has correct permissions (644)
- [ ] Contact IONOS to enable `mod_rewrite`

If styles/images don't load:
- [ ] Clear browser cache (Ctrl+Shift+Delete)
- [ ] Verify all files uploaded
- [ ] Check file paths in HTML

## Performance

- [ ] Test page load speed
- [ ] Check that assets are compressed
- [ ] Verify caching headers are set

## Security

- [ ] Remove any sensitive data from code
- [ ] Verify environment variables are not exposed
- [ ] Check that `.env` file is NOT uploaded
