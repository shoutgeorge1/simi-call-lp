# simi-call-lp

Mobile-first landing page for Simi Doctors Aesthetics & Medical - optimized for PPC traffic and phone conversions.

## Features

- Mobile-first responsive design
- Sticky phone header for easy calling
- Gold and navy blue gradient color scheme
- Prominent discount displays
- Multiple call-to-action variations
- Single HTML file with inline CSS
- All tracking scripts included (GTM, GA, Google Ads, Clarity, TikTok, Klaviyo)
- Fake header and footer for complete website appearance
- **CallRail DNI integration** for dynamic number insertion
- **GA4 click-to-call tracking** for conversion measurement

## Project Structure

```
simi-call-lp/
├── index.html          # Main HTML file
├── images/            # Image assets
├── qa/                # QA checklist and testing docs
├── README.md          # This file
└── CALLRAIL_SETUP.md  # CallRail configuration guide
```

## Phone Number

**Baseline:** (805) 526-8360  
**Call Extension (Google Ads only):** (805) 301-6977

## Setup

### CallRail Configuration

Before deploying, you need to configure CallRail DNI:

1. Get your CallRail credentials from: CallRail Dashboard > Settings > Install > Dynamic Number Insertion
2. Open `index.html` and replace:
   - `REPLACE_COMPANY_ID` with your CallRail Company ID
   - `REPLACE_KEY` with your CallRail Script Key

See `CALLRAIL_SETUP.md` for detailed instructions.

## Deployment

Deployed on Vercel:
- **Production:** https://simidoctor-calls.vercel.app/
- **GitHub Repo:** https://github.com/shoutgeorge1/simi-call-lp

## Local Development

Simply open `index.html` in a web browser or use a local server:

```bash
# Using Python
python -m http.server 8000

# Using Node.js (http-server)
npx http-server

# Using PHP
php -S localhost:8000
```

Then visit `http://localhost:8000` in your browser.

## Technologies Used

- HTML5
- CSS3 (with responsive design)
- JavaScript (for analytics and tracking)
- CallRail DNI
- Google Analytics 4

## Contact Information

- Phone: (805) 526-8360
- Location: 2840 E Los Angeles Avenue, Simi Valley, CA 93065

## Testing

See `/qa/README.md` for comprehensive QA checklist and testing procedures.
