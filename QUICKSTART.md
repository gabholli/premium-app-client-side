# 🚀 Quick Setup Guide

## Step-by-Step (5 Minutes)

### 1️⃣ Get Your API Keys

Go to [Google Cloud Console](https://console.cloud.google.com/) → APIs & Services → Credentials

**Create Key 1 (Public - for autocomplete):**
- Name: Premium App Places
- Restriction: HTTP referrers → `premium-app.netlify.app/*`, `localhost:*`
- APIs: Places API only
- ✅ Copy this key

**Create Key 2 (Secret - for verification):**
- Name: Premium App Geocoding  
- Restriction: None
- APIs: Geocoding API only
- ✅ Copy this key

### 2️⃣ Edit index.html

Line 722:
```javascript
// Replace YOUR_PLACES_API_KEY_HERE with Key 1 (Public)
<script src="https://maps.googleapis.com/maps/api/js?key=AIzaSy...KEY1&libraries=places"></script>
```

### 3️⃣ Deploy to Netlify

**Option A - Drag & Drop:**
1. Zip all files
2. Go to [app.netlify.com](https://app.netlify.com)
3. Drag ZIP file to deploy

**Option B - GitHub:**
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin YOUR_GITHUB_URL
git push -u origin main
```
Then connect GitHub repo to Netlify

### 4️⃣ Add Environment Variable

In Netlify:
1. Site Settings → Environment Variables
2. Add variable:
   - Key: `GOOGLE_MAPS_API_KEY`
   - Value: YOUR KEY 2 (Secret Geocoding key)
3. Save

### 5️⃣ Redeploy

Deploys → Trigger deploy → Clear cache and deploy site

### 6️⃣ Test!

Visit your site and test:
- ✅ Type address (autocomplete)
- ✅ Click "Verify Address"
- ✅ Should say "Address verified successfully"

## ✅ Done!

Your app is now live and secure! 🎉

## 🆘 Not Working?

**Autocomplete not showing?**
- Check Key 1 is in index.html line 722
- Make sure Places API is enabled
- Check domain restriction includes your Netlify URL

**Verification failing?**
- Check Key 2 is in Netlify environment variables
- Make sure Geocoding API is enabled
- Redeploy after adding environment variable

**Still stuck?**
Check the full README.md for detailed troubleshooting!
