# QA Checklist: CallRail DNI + GA4 Integration

## Pre-Deployment Checklist

### 1. CallRail Configuration
- [ ] Replace `REPLACE_COMPANY_ID` and `REPLACE_KEY` in `index.html` with actual values from CallRail
  - Location: CallRail Dashboard > Settings > Install > Dynamic Number Insertion
  - The script is located in the `<head>` section around line 110-118
- [ ] Verify CallRail Website Pool is active with 4-5 tracking numbers (805 area code)
- [ ] Confirm CallRail → Google Ads integration is connected
- [ ] Confirm CallRail → GA4 integration is connected

### 2. Google Ads Configuration
- [ ] Verify call extension/asset uses **(805) 301-6977** (CallRail tracking number)
- [ ] Confirm call extension is active in Google Ads campaigns
- [ ] **DO NOT** hard-code (805) 301-6977 on the website - it's for Ads only

### 3. GA4 Configuration
- [ ] Verify GA4 Measurement ID `G-DDS4W8SECB` is correct
- [ ] In GA4 → Admin → Conversions, mark `callrail_call` event as a conversion (if CallRail integration is set up)
- [ ] Import the conversion event into Google Ads

---

## Post-Deployment Testing

### Test 1: CallRail DNI Number Swap
**Objective:** Verify phone numbers swap to tracking numbers for Google Ads traffic

**Steps:**
1. Open the site in **Incognito/Private browsing mode**
2. Append `?gclid=test` to the URL: `https://simidoctor-calls.vercel.app/?gclid=test`
3. Wait 2-3 seconds for CallRail script to load
4. **Expected Result:** 
   - All visible phone numbers should swap from `(805) 526-8360` to a tracking number from the pool (e.g., `(805) 301-6977` or another 805 number)
   - Numbers should remain swapped on scroll/interaction

**How to Verify:**
- Inspect any phone number element in DevTools
- Check that the text content and `href` attribute have changed
- Verify the new number is from your CallRail pool

---

### Test 2: GA4 click_to_call Event
**Objective:** Verify phone clicks are tracked in GA4

**Steps:**
1. Open the site in **Incognito mode** with `?gclid=test`
2. Open **GA4 DebugView**:
   - Go to GA4 → Admin → DebugView
   - Or use Chrome extension: [Google Analytics Debugger](https://chrome.google.com/webstore/detail/google-analytics-debugger/jnkmfdileelhofjcijamephohjechhna)
3. Click any phone number link on the page
4. **Expected Result:**
   - Event `click_to_call` appears in DebugView within 1-2 seconds
   - Event parameters include:
     - `link_url`: The tel: link that was clicked
     - `link_text`: The visible text of the link

**How to Verify:**
- Check GA4 DebugView for the event
- Verify event parameters are populated correctly

---

### Test 3: CallRail Call Tracking
**Objective:** Verify calls are tracked in CallRail with correct source attribution

**Steps:**
1. Open the site in **Incognito mode** with `?gclid=test`
2. Wait for number swap (2-3 seconds)
3. Place a **test call** from the swapped number (if allowed/test environment)
4. **Expected Result:**
   - Call appears in **CallRail → Activity** within 1-2 minutes
   - Call shows **Source = Google Ads** (because of `gclid=test` parameter)
   - Call shows the tracking number that was displayed

**How to Verify:**
- Log into CallRail Dashboard
- Navigate to Activity/Recent Calls
- Find the test call and verify source attribution

---

### Test 4: GA4 Call Event (if CallRail → GA4 integration is active)
**Objective:** Verify call events flow from CallRail to GA4

**Steps:**
1. Place a test call (as in Test 3)
2. Wait 2-5 minutes for event propagation
3. **Expected Result:**
   - Event `callrail_call` (or configured event name) appears in GA4
   - Event shows in GA4 → Reports → Realtime or Events

**How to Verify:**
- Check GA4 Realtime reports
- Or check GA4 → Events for the call event

---

### Test 5: Baseline Number Display (Non-Ads Traffic)
**Objective:** Verify baseline number shows for non-Google Ads traffic

**Steps:**
1. Open the site in **Incognito mode** WITHOUT `?gclid=test`
2. Wait 2-3 seconds
3. **Expected Result:**
   - Phone numbers display as baseline: `(805) 526-8360`
   - Numbers do NOT swap (no Google Ads traffic detected)

**How to Verify:**
- Inspect phone number elements
- Verify they remain as `(805) 526-8360`

---

### Test 6: Mobile Device Testing
**Objective:** Verify functionality on mobile devices

**Steps:**
1. Test on actual mobile device or Chrome DevTools mobile emulation
2. Test both with and without `?gclid=test`
3. **Expected Result:**
   - Number swapping works on mobile
   - Clicking phone numbers triggers calls correctly
   - `click_to_call` events fire on mobile taps

---

## Rollback Instructions

If CallRail DNI needs to be disabled immediately:

1. **Quick Rollback:**
   - Comment out or remove the CallRail script block (lines ~107-118 in `index.html`)
   - Redeploy to Vercel
   - Phone numbers will revert to baseline `(805) 526-8360`

2. **Partial Rollback (keep tracking, disable swaps):**
   - Remove `js-swap tel` classes from phone number elements
   - Keep CallRail script (for call tracking from other sources)
   - Numbers will display baseline but calls may still be tracked

3. **GA4 remains intact** - no changes needed for GA4 rollback

---

## Troubleshooting

### Numbers Not Swapping
- **Check:** CallRail script is loading (Network tab in DevTools)
- **Check:** Company ID and Script Key are correct
- **Check:** Website Pool is active in CallRail
- **Check:** `gclid` parameter is present in URL
- **Check:** No JavaScript errors in console

### click_to_call Events Not Firing
- **Check:** GA4 script is loading (`gtag` function exists)
- **Check:** Browser console for JavaScript errors
- **Check:** GA4 DebugView is connected
- **Check:** Event is not blocked by ad blockers

### Calls Not Showing in CallRail
- **Check:** CallRail integration is active
- **Check:** Tracking number is in active pool
- **Check:** Call was placed from swapped number (not baseline)
- **Check:** Wait 2-5 minutes for call to appear

---

## Notes

- **Call Extension Number:** (805) 301-6977 is ONLY used in Google Ads call extensions, NOT on the website
- **Baseline Number:** (805) 526-8360 is displayed on-site and gets swapped by CallRail for Ads traffic
- **Consent Mode:** CallRail DNI works regardless of consent banner settings (it's not ad-cookie dependent)

