# CallRail Setup Guide - Idiot Proof

## What is CallRail?
CallRail tracks which ads/emails/websites generate phone calls. It gives you a special tracking phone number that forwards to your real number, and shows you exactly where calls came from.

---

## Step 1: Create CallRail Account

1. Go to: https://www.callrail.com/
2. Click "Start Free Trial" or "Sign Up"
3. Enter your email and create password
4. Choose a plan (start with the basic plan)

---

## Step 2: Add Your Real Phone Number

1. Log into CallRail dashboard
2. Go to **Settings** → **Numbers** → **Add Number**
3. Click **"Add Your Existing Number"**
4. Enter: **(805) 526-8360**
5. Verify the number (they'll call or text you a code)
6. ✅ Your real number is now in CallRail

---

## Step 3: Create a Web Pool (This is the Magic)

**What is a Web Pool?** It's a group of tracking numbers that CallRail automatically swaps on your website to track which pages/ads generate calls.

1. In CallRail dashboard, go to **Numbers** → **Pools**
2. Click **"Create Pool"**
3. Name it: **"Simi Doctors Landing Page"**
4. Choose **"Web Pool"** (not phone pool)
5. Select your real number: **(805) 526-8360**
6. Click **"Create Pool"**

---

## Step 4: Get Your Tracking Phone Number

1. After creating the pool, CallRail will give you a tracking number
2. It will look like: **(805) XXX-XXXX** (local number)
3. **Copy this number** - you'll need it!

---

## Step 5: Install CallRail on Your Landing Page

### Option A: JavaScript Snippet (Easiest)

1. In CallRail, go to **Settings** → **Integrations** → **JavaScript**
2. Copy the JavaScript code (looks like this):
   ```javascript
   <script type="text/javascript" src="//cdn.callrail.com/companies/XXXXX/XXXXX/12/swap.js"></script>
   ```

3. Open your `index.html` file
4. Find the `</head>` tag (near the top, after all the other scripts)
5. **Paste the CallRail code RIGHT BEFORE** `</head>`
6. Save the file
7. Push to GitHub (the changes will auto-deploy to Vercel)

### Option B: Manual Number Swap (If JavaScript doesn't work)

1. In CallRail, go to your Web Pool
2. Get the tracking number from the pool
3. In your `index.html`, find ALL instances of: `(805) 526-8360`
4. Replace them with your CallRail tracking number
5. Keep the `tel:8055268360` links as-is (CallRail will handle the swap)

---

## Step 6: Test It

1. Visit your landing page: https://simidoctor-calls.vercel.app/
2. Check if the phone number shows your CallRail tracking number
3. Call the number - it should ring your real phone: (805) 526-8360
4. In CallRail dashboard, you should see the call appear

---

## Step 7: Set Up Source Tracking (Track Where Calls Come From)

1. In CallRail, go to **Settings** → **Source Tracking**
2. Enable **"UTM Parameters"** (this tracks Google Ads, Facebook, etc.)
3. Enable **"First Touch Attribution"** (shows the first place someone saw you)
4. Save settings

---

## Step 8: Connect Google Ads (Optional but Recommended)

1. In CallRail, go to **Settings** → **Integrations** → **Google Ads**
2. Click **"Connect Google Ads"**
3. Sign in with your Google Ads account
4. Authorize CallRail
5. ✅ Now your Google Ads will show call data!

---

## What You'll See in CallRail

After setup, you can see:
- ✅ Which pages on your site generated calls
- ✅ Which ads/emails sent people to your site
- ✅ Call recordings (if enabled)
- ✅ Call transcripts
- ✅ Call duration and outcome
- ✅ Which keywords/ads work best

---

## Important Notes

1. **Keep your real number private** - only use the CallRail tracking number on your website
2. **The tracking number forwards to your real number** - you answer calls normally
3. **Calls are free** - CallRail charges per tracked call, not per minute
4. **Test before going live** - make sure calls work before sending traffic

---

## Troubleshooting

**Problem:** Phone number not swapping on website
- **Fix:** Make sure JavaScript code is in the `<head>` section, not at the bottom

**Problem:** Calls not forwarding
- **Fix:** Check that your real number is verified in CallRail settings

**Problem:** Can't see call data
- **Fix:** Wait 5-10 minutes, data can take time to appear

---

## Need Help?

CallRail Support: 1-888-858-4594
Or email: support@callrail.com


