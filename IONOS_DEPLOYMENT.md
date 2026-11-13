# IONOS Starter Plan Deployment Guide

This project has been configured for static hosting on IONOS Starter Plan.

## Prerequisites

- Node.js 18+ or Bun installed locally
- IONOS Starter Plan account with FTP/SFTP access
- An FTP client (FileZilla, WinSCP, or similar)

## Build Instructions

### 1. Install Dependencies

```bash
# Using npm
npm install

# Or using bun
bun install
```

### 2. Build the Project

```bash
# Using npm
npm run build

# Or using bun
bun run build
```

This will create a `dist` folder with all the static files ready for deployment.

## Deployment Steps

### 1. Connect via FTP

1. Open your FTP client
2. Connect to your IONOS hosting using:
   - **Host**: Your domain or FTP server address (from IONOS control panel)
   - **Username**: Your FTP username (from IONOS control panel)
   - **Password**: Your FTP password (from IONOS control panel)
   - **Port**: 21 (or 22 for SFTP)

### 2. Upload Files

1. Navigate to the `public_html` or `www` folder on your IONOS server
2. Upload all files from the `dist` folder to this directory
3. **Important**: Make sure the `.htaccess` file is uploaded (it's hidden by default)
   - In FileZilla: View → Show hidden files
   - In WinSCP: View → Show hidden files

### 3. Verify Deployment

1. Visit your domain in a browser
2. Test navigation between pages
3. Check that all images and styles load correctly

## Important Notes

### .htaccess Configuration

The `.htaccess` file in the `public` folder handles:
- **SPA Routing**: Routes all requests to `index.html` for client-side routing
- **Compression**: Gzip compression for faster loading
- **Caching**: Browser caching for static assets
- **Security Headers**: Basic security headers

This file is **critical** for the site to work properly. Make sure it's uploaded to the root of your hosting.

### Environment Variables

If you're using Supabase or other services, create a `.env` file locally with:

```
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_key
```

These will be embedded in the build during `npm run build`.

### Limitations on IONOS Starter Plan

- **No server-side rendering**: This is a static SPA
- **No backend API**: Use Supabase or similar for backend needs
- **No Node.js runtime**: Cannot run server-side code
- **File size limits**: Check your plan's storage limits

## Troubleshooting

### Pages show 404 errors

- Ensure `.htaccess` is uploaded to the root directory
- Check that `mod_rewrite` is enabled on your IONOS account
- Contact IONOS support if mod_rewrite is disabled

### Styles or images not loading

- Clear browser cache (Ctrl+Shift+Delete)
- Verify all files were uploaded correctly
- Check file permissions (should be 644 for files, 755 for directories)

### Site loads but routing doesn't work

- Verify `.htaccess` is in the correct location
- Check that the file has correct line endings (LF, not CRLF)
- Ensure `RewriteEngine` is enabled in your IONOS control panel

## Local Development

To test locally before deployment:

```bash
npm run dev
```

This starts a development server at `http://localhost:5173`

## Production Optimization

The build is already optimized with:
- Code splitting for vendor and UI libraries
- Minification and tree-shaking
- Asset optimization
- Gzip compression configuration

## Support

For IONOS-specific issues:
- Contact IONOS support: https://www.ionos.com/help
- Check IONOS documentation for your plan

For application issues:
- Check browser console for errors (F12)
- Verify all dependencies are correctly installed
