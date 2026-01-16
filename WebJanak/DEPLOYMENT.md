# WebJanak - Vercel Deployment Guide

## 🚀 Quick Deploy

### Option 1: Deploy via Vercel CLI (Recommended)

1. **Install Vercel CLI**
```bash
npm install -g vercel
```

2. **Login to Vercel**
```bash
vercel login
```

3. **Deploy from project root**
```bash
cd "d:\text to react ui"
vercel
```

4. **Follow the prompts**
- Set up and deploy: `Y`
- Which scope: Select your account
- Link to existing project: `N`
- Project name: `webjanak` (or your choice)
- Directory: `./` (root)
- Override settings: `N`

5. **Set environment variables**
```bash
vercel env add GEMINI_API_KEY
# Paste your API key when prompted
# Select Production, Preview, Development
```

6. **Deploy to production**
```bash
vercel --prod
```

### Option 2: Deploy via Vercel Dashboard

1. **Push code to GitHub**
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/webjanak.git
git push -u origin main
```

2. **Import to Vercel**
- Go to [vercel.com](https://vercel.com)
- Click "Add New Project"
- Import your GitHub repository
- Configure project:
  - **Framework Preset**: Vite
  - **Root Directory**: `./`
  - **Build Command**: `npm run build`
  - **Output Directory**: `client/dist`

3. **Add Environment Variables**
In Vercel Dashboard → Settings → Environment Variables:
```
GEMINI_API_KEY = your_gemini_api_key_here
NODE_ENV = production
PORT = 3000
```

4. **Deploy**
Click "Deploy" and wait for build to complete

## ⚙️ Configuration Files

### 1. `vercel.json` (Already created)
```json
{
  "version": 2,
  "builds": [
    {
      "src": "client/package.json",
      "use": "@vercel/static-build",
      "config": { "distDir": "dist" }
    },
    {
      "src": "src/server.ts",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    { "src": "/api/(.*)", "dest": "/src/server.ts" },
    { "src": "/generated/(.*)", "dest": "/src/server.ts" },
    { "src": "/(.*)", "dest": "/client/dist/$1" }
  ]
}
```

### 2. Update API URLs in Frontend

**Important**: Change API URLs from localhost to relative paths:

**Before** (in `client/src/App.jsx`):
```javascript
const response = await fetch('http://localhost:3000/api/generate', ...)
```

**After**:
```javascript
const response = await fetch('/api/generate', ...)
```

This makes it work on both local and production.

### 3. Build Scripts

Backend build (already configured):
```bash
npm run build  # Compiles TypeScript to dist/
```

Frontend build (already configured):
```bash
cd client && npm run build  # Creates client/dist/
```

## 🔧 Post-Deployment

### Verify Deployment

1. **Check frontend**: `https://your-project.vercel.app`
2. **Test API**: `https://your-project.vercel.app/api/projects`
3. **Test generation**: Use the UI to generate a project

### Common Issues & Fixes

**Issue 1: API endpoints not working**
- Solution: Ensure all API calls use relative paths (`/api/...` not `http://localhost:3000/api/...`)

**Issue 2: Environment variables not loaded**
- Solution: Add them in Vercel Dashboard → Settings → Environment Variables
- Redeploy after adding variables

**Issue 3: Build fails**
- Solution: Check build logs in Vercel dashboard
- Ensure all dependencies are in `package.json`
- Run `npm run build` locally first to test

**Issue 4: File system operations fail**
- Solution: Vercel has read-only filesystem. Use Vercel KV or external storage for generated files
- Alternative: Store in database (MongoDB, Supabase)

## 📊 Monitoring

- **Analytics**: Vercel Dashboard → Analytics
- **Logs**: Vercel Dashboard → Deployments → Functions tab
- **Performance**: Check Web Vitals in Vercel dashboard

## 🔄 Continuous Deployment

Once connected to GitHub:
1. Push code to `main` branch
2. Vercel auto-deploys
3. Preview deployments for PRs

```bash
git add .
git commit -m "Update feature"
git push origin main
# Vercel automatically deploys!
```

## 🌐 Custom Domain (Optional)

1. Go to Vercel Dashboard → Settings → Domains
2. Add your domain: `webjanak.gov.in`
3. Update DNS records as instructed
4. SSL certificate auto-provisioned

## 💡 Pro Tips

1. **Environment Variables**: Keep secrets in Vercel, not in code
2. **Preview Deployments**: Every Git branch gets a preview URL
3. **Rollbacks**: Instant rollback to previous deployment in dashboard
4. **Edge Functions**: Consider Vercel Edge for faster response times
5. **Logs**: Use `console.log()` - visible in Vercel function logs

## 🚨 Important Notes

### File Storage Limitation
Vercel has a **read-only filesystem**. Your current implementation saves generated projects to `generated-projects/` which won't persist.

**Solutions**:
1. **Vercel Blob Storage** (Recommended)
2. **External Storage** (AWS S3, Cloudinary)
3. **Database** (MongoDB, Supabase)
4. **Vercel KV** (for metadata)

### Recommended: Migrate to Vercel Blob

```bash
npm install @vercel/blob
```

Update `src/server.ts`:
```typescript
import { put } from '@vercel/blob';

// Instead of fs.writeFile
const blob = await put(`projects/${projectId}/index.html`, code, {
  access: 'public',
});
```

## 📝 Deployment Checklist

- [ ] Code pushed to GitHub
- [ ] Environment variables set in Vercel
- [ ] API URLs changed to relative paths
- [ ] Local build tested (`npm run build`)
- [ ] Vercel project created
- [ ] First deployment successful
- [ ] API endpoints tested
- [ ] Frontend tested on mobile
- [ ] Custom domain configured (optional)
- [ ] Monitoring/analytics enabled

## 🎯 Next Steps After Deployment

1. **Test thoroughly**: Try all features
2. **Monitor logs**: Check for errors
3. **Set up alerts**: Get notified of issues
4. **Add analytics**: Track usage
5. **Configure CDN**: Already done by Vercel!

---

**Need Help?**
- Vercel Docs: https://vercel.com/docs
- Vercel Support: https://vercel.com/support
- Community: https://github.com/vercel/vercel/discussions
