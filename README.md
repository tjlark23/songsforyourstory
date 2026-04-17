# Songs For Your Story
Live: https://songsforyourstory.com

Custom song creation website. Radio-quality, fully personalized songs for birthdays, weddings, retirements, corporate events, and more.

## Stack
- Static HTML/CSS/JS (single-file architecture)
- Fonts: Instrument Serif + DM Sans (Google Fonts)
- Payments: Stripe Payment Links
- Forms: Web3Forms
- Audio: Hosted on GitHub (tjlark23/SFYS-music repo)
- Deployment: Cloudflare Pages (project: songsforyourstory)
- Domain: songsforyourstory.com (Cloudflare DNS)

## Files
- `index.html` - Main homepage
- `showcase.html` - "From Our Studio" showcase page
- `robots.txt` - Search engine crawl rules
- `sitemap.xml` - Site map for search engines

## Deploy
```bash
npx wrangler pages deploy . --project-name=songsforyourstory
```
