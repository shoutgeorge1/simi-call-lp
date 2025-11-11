# CallRail DNI Setup Instructions

## Quick Setup

The CallRail Dynamic Number Insertion (DNI) script has been added to the site, but requires your CallRail credentials to be configured.

## Step 1: Get Your CallRail Credentials

1. Log into your CallRail account
2. Navigate to **Settings** → **Install** → **Dynamic Number Insertion**
3. You'll see two values:
   - **Company ID** (e.g., `123456789`)
   - **Script Key** (e.g., `abc123def456`)

## Step 2: Update index.html

1. Open `index.html` in your editor
2. Find the CallRail script block (around line 110-118)
3. Replace the placeholders:
   - Replace `REPLACE_COMPANY_ID` with your actual Company ID
   - Replace `REPLACE_KEY` with your actual Script Key

**Before:**
```html
"https://cdn.callrail.com/companies/REPLACE_COMPANY_ID/REPLACE_KEY/callrail.min.js"
```

**After (example):**
```html
"https://cdn.callrail.com/companies/123456789/abc123def456/callrail.min.js"
```

## Step 3: Verify Website Pool Configuration

1. In CallRail, go to **Numbers** → **Website Pools**
2. Ensure you have a pool with 4-5 tracking numbers (805 area code)
3. The pool should be **Active**
4. Verify the pool is assigned to your website/domain

## Step 4: Configure Integrations (Optional but Recommended)

### CallRail → Google Ads Integration
1. In CallRail, go to **Integrations** → **Google Ads**
2. Connect your Google Ads account
3. This allows call data to flow to Google Ads for optimization

### CallRail → GA4 Integration
1. In CallRail, go to **Integrations** → **Google Analytics 4**
2. Connect your GA4 property (G-DDS4W8SECB)
3. This sends call events to GA4

### GA4 → Google Ads Conversion Import
1. In GA4, go to **Admin** → **Conversions**
2. Mark the `callrail_call` event as a conversion
3. In Google Ads, go to **Tools & Settings** → **Conversions**
4. Import the conversion from GA4

## Step 5: Test the Implementation

See `/qa/README.md` for detailed testing instructions.

Quick test:
1. Deploy the updated `index.html` to Vercel
2. Visit the site with `?gclid=test` appended to the URL
3. Wait 2-3 seconds
4. Verify phone numbers swap to tracking numbers

## Important Notes

- **Call Extension Number:** The number **(805) 301-6977** should ONLY be used in Google Ads call extensions/assets, NOT hard-coded on the website
- **Baseline Number:** The website displays **(805) 526-8360** which gets swapped by CallRail for Google Ads traffic
- **Consent Mode:** CallRail DNI works regardless of consent banner settings

## Support

If you encounter issues:
1. Check the QA checklist in `/qa/README.md`
2. Verify CallRail script is loading (browser DevTools → Network tab)
3. Check browser console for JavaScript errors
4. Verify credentials are correct in the script URL

