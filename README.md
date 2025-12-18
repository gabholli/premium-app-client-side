# Secure Premium App with Netlify Backend Proxy

🔒 **This version uses a backend proxy to keep your Google Maps API key completely secure!**

## 📁 Project Structure

```
premium-app-secure/
├── index.html                      # Main application file
├── netlify/
│   └── functions/
│       └── geocode.js              # Secure backend proxy function
├── package.json                    # Dependencies for Netlify functions
├── netlify.toml                    # Netlify configuration
└── README.md                       # This file
```

## 🔐 Security Features

✅ **API key completely hidden** (stored in Netlify environment variables)
✅ **Rate limiting** (10 requests per minute per IP)
✅ **Input validation** (prevents malicious requests)
✅ **Two-key strategy** (public key for autocomplete, secret key for verification)
✅ **Caching** (reduces API calls)

## 🚀 Setup Instructions

### Step 1: Create Two Google Maps API Keys

You need TWO separate API keys for maximum security:

#### Key 1: Public Key (for Places Autocomplete Widget)
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Navigate to: **APIs & Services → Credentials**
3. Click **"+ Create Credentials" → "API Key"**
4. Name it: **"Premium App - Places (Public)"**
5. Click **"Edit API key"**
6. **Application restrictions:**
   - Select: **HTTP referrers (websites)**
   - Add referrers:
     ```
     localhost:*
     127.0.0.1:*
     premium-app.netlify.app/*
     ```
7. **API restrictions:**
   - Select: **Restrict key**
   - Enable ONLY: **Places API** ✅
8. Click **"Save"**
9. Copy this key for later (Key 1)

#### Key 2: Secret Key (for Geocoding via Backend)
1. Create another API key
2. Name it: **"Premium App - Geocoding (Secret)"**
3. Click **"Edit API key"**
4. **Application restrictions:**
   - Select: **None** (server-side use)
5. **API restrictions:**
   - Select: **Restrict key**
   - Enable ONLY: **Geocoding API** ✅
6. Click **"Save"**
7. Copy this key for later (Key 2)

### Step 2: Enable Required APIs

Make sure these APIs are enabled:
1. Go to **APIs & Services → Library**
2. Search and enable:
   - **Places API** ✅
   - **Geocoding API** ✅

### Step 3: Set Up Billing

1. Go to **Billing** in Google Cloud Console
2. Add a billing account (credit card required)
3. Don't worry - you get **$200 FREE credit per month**
4. Set budget alerts at $10, $50, $100

### Step 4: Deploy to Netlify

#### Option A: Drag & Drop (Easiest)

1. **Prepare your files:**
   - Edit `index.html` line 722:
     ```javascript
     <script src="https://maps.googleapis.com/maps/api/js?key=YOUR_PLACES_API_KEY_HERE&libraries=places"></script>
     ```
     Replace `YOUR_PLACES_API_KEY_HERE` with your **Key 1 (Public Places Key)**

2. **Create a ZIP file** containing:
   - `index.html`
   - `netlify/` folder with `functions/geocode.js`
   - `package.json`
   - `netlify.toml`

3. **Go to [Netlify](https://app.netlify.com/)**
   - Sign up/login
   - Click **"Add new site" → "Deploy manually"**
   - Drag your ZIP file or the entire folder

4. **Configure Environment Variable:**
   - Go to: **Site settings → Environment variables**
   - Click **"Add a variable"**
   - **Key:** `GOOGLE_MAPS_API_KEY`
   - **Value:** Your **Key 2 (Secret Geocoding Key)**
   - **Scopes:** Select all ✅
   - Click **"Create variable"**

5. **Redeploy:**
   - Go to **Deploys** tab
   - Click **"Trigger deploy" → "Clear cache and deploy site"**

6. **Done!** Your site is live at `https://your-site-name.netlify.app`

#### Option B: GitHub Integration (Recommended for Updates)

1. **Create a GitHub repository:**
   ```bash
   cd premium-app-secure
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/yourusername/premium-app-secure.git
   git push -u origin main
   ```

2. **Connect to Netlify:**
   - Go to [Netlify](https://app.netlify.com/)
   - Click **"Add new site" → "Import an existing project"**
   - Choose **"GitHub"**
   - Select your repository
   - **Build settings:**
     - Build command: (leave empty)
     - Publish directory: `.`
   - Click **"Deploy site"**

3. **Add Environment Variable:**
   - Go to: **Site settings → Environment variables**
   - Add: `GOOGLE_MAPS_API_KEY` = **Key 2 (Secret)**

4. **Update index.html:**
   - Edit line 722 with your **Key 1 (Public Places Key)**
   - Push to GitHub:
     ```bash
     git add index.html
     git commit -m "Add public API key"
     git push
     ```
   - Netlify auto-deploys! ✅

### Step 5: Update Domain Restrictions

After deploying, update your Public API key restrictions:

1. Go to Google Cloud Console → Credentials
2. Edit **Key 1 (Public Places Key)**
3. Add your Netlify domain to HTTP referrers:
   ```
   your-site-name.netlify.app/*
   ```
4. Save

## 🧪 Testing

### Test Locally:

1. **Install dependencies:**
   ```bash
   npm install netlify-cli -g
   npm install
   ```

2. **Set up local environment variable:**
   Create `.env` file:
   ```
   GOOGLE_MAPS_API_KEY=your_secret_key_2_here
   ```

3. **Update index.html** with your Public Key (Key 1)

4. **Run locally:**
   ```bash
   netlify dev
   ```
   Opens at `http://localhost:8888`

5. **Test features:**
   - ✅ Address autocomplete dropdown
   - ✅ Manual address entry
   - ✅ Address verification
   - ✅ Premium calculation

### Test on Netlify:

1. Visit your deployed site
2. Test all features
3. Check browser console (F12) for any errors
4. Monitor usage in Google Cloud Console

## 📊 Monitoring

### Check API Usage:

1. **Google Cloud Console:**
   - Go to: **APIs & Services → Dashboard**
   - Check requests per day for:
     - Places API (autocomplete)
     - Geocoding API (verification)

2. **Netlify Functions:**
   - Go to: **Functions** tab in Netlify
   - Monitor invocations
   - Check for errors

### Set Alerts:

1. **Google Cloud:**
   - Billing → Budgets & alerts
   - Create alerts at $10, $50, $100

2. **Netlify:**
   - Free tier: 125,000 function requests/month
   - Alerts automatically sent if approaching limit

## 🔧 Troubleshooting

### "API key not valid" Error

**Problem:** Public key (Key 1) not working in autocomplete

**Solutions:**
- ✅ Make sure Places API is enabled
- ✅ Check domain restriction includes your Netlify URL
- ✅ Wait 5 minutes for API key changes to propagate
- ✅ Clear browser cache

### "Failed to verify address" Error

**Problem:** Backend geocoding not working

**Solutions:**
- ✅ Check environment variable is set in Netlify
- ✅ Make sure it's named exactly: `GOOGLE_MAPS_API_KEY`
- ✅ Ensure Geocoding API is enabled for Key 2
- ✅ Redeploy site after adding environment variable
- ✅ Check Netlify function logs for errors

### "Too many requests" Error

**Problem:** Rate limit reached

**Solution:**
- ✅ This is working as intended (security feature)
- ✅ Wait 1 minute and try again
- ✅ Adjust rate limit in `netlify/functions/geocode.js` if needed

### Local Testing Not Working

**Problem:** Functions don't work with `netlify dev`

**Solutions:**
- ✅ Make sure you have `.env` file with secret key
- ✅ Run `npm install` first
- ✅ Use `netlify dev` not `python -m http.server`
- ✅ Check `.env` file is in project root

## 📈 Cost Breakdown

### With 1,000 Users/Month:

**Google Maps API:**
- Places autocomplete: ~1,000 sessions
- Geocoding: ~1,000 requests
- **Cost: $0** (within free tier)

**Netlify:**
- Functions: ~1,000 invocations
- **Cost: $0** (within free tier)

**Total: $0/month** ✅

### Scaling:

| Monthly Users | Google Cost | Netlify Cost | Total |
|---------------|-------------|--------------|-------|
| 1,000 | $0 | $0 | $0 |
| 10,000 | $0 | $0 | $0 |
| 25,000 | $0 | $0 | $0 |
| 50,000 | ~$195 | $0 | ~$195 |
| 100,000 | ~$580 | $0 | ~$580 |

## 🛡️ Security Comparison

| Feature | Without Backend | With Backend (This Setup) |
|---------|-----------------|---------------------------|
| API key visible | ❌ Yes | ✅ No |
| Can be stolen | ❌ Yes | ✅ No |
| Rate limiting | ❌ No | ✅ Yes (10/min/IP) |
| Input validation | ❌ No | ✅ Yes |
| Quota protection | ⚠️ Partial | ✅ Full |
| **Security Level** | ⚠️ Medium | ✅ High (9/10) |

## 📝 Customization

### Adjust Rate Limit:

Edit `netlify/functions/geocode.js` line 11:
```javascript
// Change from 10 to your desired limit
if (count >= 10) {  // requests per minute
```

### Add Caching:

The function already includes 1-hour cache headers. To adjust:

Edit `netlify/functions/geocode.js` line 96:
```javascript
'Cache-Control': 'public, max-age=3600' // 3600 seconds = 1 hour
```

### Add Authentication:

To require a secret token from frontend:

```javascript
// In netlify/functions/geocode.js, add after line 30:
const token = event.headers['x-api-token'];
if (token !== process.env.SECRET_TOKEN) {
  return {
    statusCode: 401,
    body: JSON.stringify({ error: 'Unauthorized' })
  };
}
```

Then add `SECRET_TOKEN` to Netlify environment variables.

## 🎯 Next Steps

- [ ] Deploy to Netlify
- [ ] Add environment variable
- [ ] Test thoroughly
- [ ] Set up billing alerts
- [ ] Monitor usage weekly
- [ ] Consider custom domain

## 🆘 Support

If you encounter issues:

1. Check browser console (F12) for errors
2. Check Netlify function logs
3. Verify environment variables are set
4. Ensure both APIs are enabled
5. Wait 5 minutes after making changes

## ✅ Success Checklist

Before going live:

- [ ] Two API keys created (Public + Secret)
- [ ] Places API enabled
- [ ] Geocoding API enabled
- [ ] Billing account set up
- [ ] Budget alerts configured
- [ ] Public key added to index.html
- [ ] Secret key added to Netlify env vars
- [ ] Domain restrictions updated
- [ ] Site deployed successfully
- [ ] Address autocomplete working
- [ ] Address verification working
- [ ] Calculator working
- [ ] Mobile responsive tested

## 📄 License

This is a secure implementation template. Use and modify as needed for your project.

---

**🔒 Your API key is now completely secure!**
