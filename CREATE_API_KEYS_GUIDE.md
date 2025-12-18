# 🔑 Step-by-Step: Creating Two Google Maps API Keys

## 📋 Prerequisites
- Google account
- Credit card (won't be charged - just for verification)
- 20 minutes

---

## PART 1: INITIAL SETUP

### Step 1: Go to Google Cloud Console

1. **Open your browser**

2. **Go to:** https://console.cloud.google.com/

3. **Sign in** with your Google account

4. **Accept terms** if this is your first time

---

### Step 2: Create a New Project

1. **Look at the top of the page**
   - You'll see a dropdown that says "Select a project" or shows a project name
   - It's next to the Google Cloud logo

2. **Click that dropdown**

3. **Click "New Project"** (top right of the popup)

4. **Fill in the form:**
   - **Project name:** `Premium App` (or any name you like)
   - **Location:** Leave as "No organization"

5. **Click "CREATE"** (blue button, bottom right)

6. **Wait 10-30 seconds**
   - You'll see a notification in the top right
   - "Creating project Premium App..."
   - Then: "Project created"

7. **Click "SELECT PROJECT"** in the notification
   - Or click the project dropdown again and select "Premium App"

✅ **Your project is now created and selected**

---

### Step 3: Enable Billing

**Why:** Google requires a credit card even for free tier

1. **Look at the left sidebar**

2. **Click the hamburger menu** (☰ three horizontal lines, top left)

3. **Scroll down and click "Billing"**

4. **You'll see one of two things:**

   **Option A: "This project has no billing account"**
   - Click "LINK A BILLING ACCOUNT"
   - Then "CREATE BILLING ACCOUNT"

   **Option B: "Enable billing for this project"**
   - Click "ENABLE BILLING"

5. **Fill in the billing form:**
   - **Country:** Select your country
   - **Name:** Your name
   - **Address:** Your address
   - **Credit card:** Your card details

6. **Check the box:** "I have read and agree to the terms"

7. **Click "START MY FREE TRIAL"** or "SUBMIT AND ENABLE BILLING"

8. **You should see:** "Your billing account is now active"

✅ **Billing enabled (you get $200 FREE per month)**

---

### Step 4: Enable Places API

1. **Click the hamburger menu** (☰) again

2. **Go to:** APIs & Services → Library
   - Or search "API Library" in the search bar at top

3. **You'll see a page full of API options**

4. **In the search box**, type: `Places API`

5. **Click on "Places API"** (should be first result)
   - Icon looks like a map pin
   - Says "Places API" underneath

6. **Click the blue "ENABLE" button**

7. **Wait 5-10 seconds**
   - Page will refresh
   - You'll see "API enabled"
   - Top will say "Places API" with a green checkmark

✅ **Places API is now enabled**

---

### Step 5: Enable Geocoding API

1. **Click "← " (back arrow)** at the top
   - Or click "API Library" in the left sidebar

2. **In the search box**, type: `Geocoding API`

3. **Click on "Geocoding API"**
   - Icon looks like a location pin with circles

4. **Click the blue "ENABLE" button**

5. **Wait 5-10 seconds**
   - Page will refresh
   - You'll see "API enabled"

✅ **Geocoding API is now enabled**

---

## PART 2: CREATE KEY 1 (PUBLIC - FOR PLACES AUTOCOMPLETE)

### Step 6: Go to Credentials Page

1. **Click the hamburger menu** (☰)

2. **Go to:** APIs & Services → Credentials

3. **You'll see a page with tabs:** Credentials, OAuth consent screen, Domain verification

---

### Step 7: Create the First API Key

1. **Click the "+ CREATE CREDENTIALS" button** (near the top)

2. **Select "API key"** from the dropdown

3. **A popup appears:**
   - Shows your API key (starts with `AIzaSy...`)
   - Says "API key created"

4. **IMMEDIATELY COPY THIS KEY:**
   - Select all the text (highlight it)
   - Copy it (Ctrl+C or Cmd+C)
   - **Paste it somewhere safe:**
     - Notepad (Windows)
     - Notes app (Mac)
     - Text file
   - **Label it:** "KEY 1 - PUBLIC - PLACES"

5. **DO NOT CLOSE THE POPUP YET**

6. **Click "RESTRICT KEY"** (blue button in the popup)
   - This takes you to the key editing page

---

### Step 8: Restrict Key 1 - Set Name

1. **You're now on the "Edit API key" page**

2. **At the very top**, find "API key name"
   - Currently says something like: "API key 1"

3. **Click in the text box**

4. **Change it to:** `Premium App - Places (Public)`

5. **Don't click Save yet** - we have more to do

---

### Step 9: Restrict Key 1 - Application Restrictions

1. **Scroll down to "Application restrictions"**

2. **You'll see 4 radio button options:**
   - ⚪ None
   - ⚪ HTTP referrers (websites)
   - ⚪ IP addresses
   - ⚪ Android apps
   - ⚪ iOS apps

3. **Select: "HTTP referrers (websites)"** ← Click this one

4. **A new section appears: "Website restrictions"**

5. **Click "+ ADD AN ITEM"**

6. **In the text box that appears, type:** `localhost:*`

7. **Click "+ ADD AN ITEM" again**

8. **Type:** `127.0.0.1:*`

9. **Click "+ ADD AN ITEM" again**

10. **Type:** `premium-app.netlify.app/*`
    - Or whatever your Netlify domain will be
    - You can update this later

**Your list should now show:**
```
localhost:*
127.0.0.1:*
premium-app.netlify.app/*
```

---

### Step 10: Restrict Key 1 - API Restrictions

1. **Scroll down further to "API restrictions"**

2. **You'll see 2 radio button options:**
   - ⚪ Don't restrict key
   - ⚪ Restrict key

3. **Select: "Restrict key"** ← Click this one

4. **A dropdown appears that says "Select APIs"**

5. **Click the dropdown**

6. **You'll see a long list of APIs**

7. **Scroll down and find "Places API"**

8. **Click the checkbox next to "Places API"** ✅
   - Should see a blue checkmark

9. **Make sure ONLY Places API is checked**
   - Scroll through to verify
   - Especially make sure "Geocoding API" is NOT checked ❌

10. **Click anywhere outside the dropdown** to close it

**You should see:**
```
API restrictions: Restrict key
Selected APIs: Places API
```

---

### Step 11: Save Key 1

1. **Scroll to the bottom of the page**

2. **Click "SAVE"** (blue button)

3. **Wait 5-10 seconds**

4. **You'll see a notification:**
   - "API key updated"
   - Or "API key saved successfully"

5. **IMPORTANT:** Wait 5 minutes for restrictions to take effect

✅ **KEY 1 IS NOW CREATED AND SECURED!**

---

## PART 3: CREATE KEY 2 (SECRET - FOR GEOCODING)

### Step 12: Create the Second API Key

1. **You're still on the Credentials page**
   - If not: Go to APIs & Services → Credentials

2. **Click "+ CREATE CREDENTIALS"** again (at the top)

3. **Select "API key"**

4. **Another popup appears with a new key**

5. **IMMEDIATELY COPY THIS KEY:**
   - It's different from Key 1!
   - Starts with `AIzaSy...` but has different characters
   - Copy it (Ctrl+C or Cmd+C)
   - **Paste it somewhere safe**
   - **Label it:** "KEY 2 - SECRET - GEOCODING"

6. **Click "RESTRICT KEY"** in the popup

---

### Step 13: Restrict Key 2 - Set Name

1. **You're now on the edit page for the second key**

2. **At the top, change "API key name" to:**
   `Premium App - Geocoding (Secret)`

3. **Don't click Save yet**

---

### Step 14: Restrict Key 2 - Application Restrictions

1. **Scroll to "Application restrictions"**

2. **Select: "None"** ← This is different from Key 1!
   - Click the "None" radio button
   - This is because Key 2 will be used server-side (in Netlify functions)
   - Server-side calls don't have domains

**Your selection should show:**
```
Application restrictions: None
```

---

### Step 15: Restrict Key 2 - API Restrictions

1. **Scroll down to "API restrictions"**

2. **Select: "Restrict key"**

3. **Click the dropdown "Select APIs"**

4. **Find "Geocoding API"** in the list

5. **Click the checkbox next to "Geocoding API"** ✅

6. **Make sure ONLY Geocoding API is checked**
   - Especially make sure "Places API" is NOT checked ❌

7. **Click outside the dropdown to close it**

**You should see:**
```
API restrictions: Restrict key
Selected APIs: Geocoding API
```

---

### Step 16: Save Key 2

1. **Scroll to the bottom**

2. **Click "SAVE"** (blue button)

3. **Wait 5-10 seconds**

4. **You'll see "API key updated"**

5. **IMPORTANT:** Wait 5 minutes for restrictions to take effect

✅ **KEY 2 IS NOW CREATED AND SECURED!**

---

## PART 4: VERIFY YOUR KEYS

### Step 17: Check Your Credentials Page

1. **Go to:** APIs & Services → Credentials

2. **Under "API Keys" section**, you should see:

```
Premium App - Places (Public)
Premium App - Geocoding (Secret)
```

3. **You should have both keys saved in your notes:**

```
KEY 1 - PUBLIC - PLACES:
AIzaSyA... (your actual key 1)

KEY 2 - SECRET - GEOCODING:
AIzaSyB... (your actual key 2)
```

✅ **Both keys created successfully!**

---

## 📋 QUICK REFERENCE

### Key 1 (Public - Places)
- **Name:** Premium App - Places (Public)
- **Use for:** Autocomplete widget in HTML
- **Restrictions:**
  - Application: HTTP referrers (websites)
  - Domains: localhost:*, 127.0.0.1:*, premium-app.netlify.app/*
  - API: Places API ONLY
- **Where it goes:** In your `index.html` file (line 722)

### Key 2 (Secret - Geocoding)
- **Name:** Premium App - Geocoding (Secret)
- **Use for:** Address verification via backend
- **Restrictions:**
  - Application: None (server-side)
  - API: Geocoding API ONLY
- **Where it goes:** Netlify environment variable (NEVER in code!)

---

## 🔍 HOW TO TELL THEM APART

**Look at your Credentials page:**

| Key Name | Application Restrictions | API Restrictions |
|----------|-------------------------|------------------|
| Premium App - Places (Public) | HTTP referrers | Places API |
| Premium App - Geocoding (Secret) | None | Geocoding API |

---

## ✅ CHECKLIST

Before moving on, make sure:

- [ ] Both API keys created
- [ ] Both keys copied and saved safely
- [ ] Key 1 restricted to: HTTP referrers + Places API
- [ ] Key 2 restricted to: None + Geocoding API
- [ ] Both keys labeled clearly in your notes
- [ ] Waited 5 minutes for restrictions to activate

---

## 🆘 TROUBLESHOOTING

### Can't find "CREATE CREDENTIALS" button

**Solution:**
- Make sure you selected your project (check dropdown at top)
- Go to: APIs & Services → Credentials
- Look near the top of the page
- Should be a blue button with "+ CREATE CREDENTIALS"

---

### Don't see "HTTP referrers" option

**Solution:**
- Make sure you're editing Key 1 (Places key)
- Under "Application restrictions"
- Should see 4-5 radio button options
- "HTTP referrers (websites)" should be one of them

---

### Can't find "Places API" in the dropdown

**Solution:**
- Make sure Places API is enabled
- Go to: APIs & Services → Library
- Search "Places API"
- Should say "Manage" (not "Enable")
- If says "Enable", click it first

---

### Restrictions not saving

**Solution:**
- Scroll all the way to bottom
- Click "SAVE" button
- Wait for "API key updated" notification
- Refresh the page
- Click the key again to verify settings saved

---

### Lost track of which key is which

**Solution:**
- Go to: APIs & Services → Credentials
- Look at the key names:
  - "Premium App - Places (Public)" = Key 1
  - "Premium App - Geocoding (Secret)" = Key 2
- Click each one to see restrictions
- Key 1 should have HTTP referrers
- Key 2 should have None

---

## 🎯 NEXT STEPS

Now that you have both keys:

1. **Use Key 1:** Put in your `index.html` file (line 722)
2. **Use Key 2:** Add to Netlify environment variables
3. **Never mix them up!**
4. **Never commit Key 2 to Git!**

---

## 📝 SAVE THIS TEMPLATE

Keep this in a safe place (NOT in Git):

```
PROJECT: Premium App
GOOGLE CLOUD PROJECT ID: [your project id]

KEY 1 - PUBLIC - PLACES (for autocomplete):
Name: Premium App - Places (Public)
Key: AIzaSyA_________________________
Restrictions: 
- HTTP referrers: localhost:*, premium-app.netlify.app/*
- API: Places API only
Use: Put in index.html line 722

KEY 2 - SECRET - GEOCODING (for verification):
Name: Premium App - Geocoding (Secret)  
Key: AIzaSyB_________________________
Restrictions:
- Application: None
- API: Geocoding API only
Use: Netlify environment variable

CREATED: [today's date]
```

---

## ✅ YOU'RE DONE!

You now have both API keys properly created and secured! 🎉

**Next:** Follow the main deployment guide to use these keys.

**Remember:**
- ✅ Key 1 goes in HTML (public, visible)
- ✅ Key 2 goes in Netlify env vars (secret, hidden)
- ✅ Never commit Key 2 to Git
- ✅ Wait 5 minutes after creating before using
