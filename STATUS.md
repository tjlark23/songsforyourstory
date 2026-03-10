# Project Status

## Last Updated: 2026-03-10
## Repo: https://github.com/tjlark23/songsforyourstory
## Live URL: https://songsforyourstory.com
## Stack: Static HTML/CSS/JS, Cloudflare Pages

## Current State
- Working: Full site live with audio players, Stripe payments, Web3Forms contact/order forms
- Working: SEO optimized per SEO Bible (canonical, OG tags, Twitter Card, JSON-LD @graph, semantic HTML, aria-labels)
- Working: robots.txt and sitemap.xml

## Last Session (2026-03-10)
- Applied SEO-only backend fixes to index.html (zero visual changes)
- Created this GitHub repo for version control
- Changes: title tag, canonical URL, OG tags, Twitter Card, JSON-LD @graph with Organization+Person+Service+FAQPage, aria-labels on nav and all sections, <main> wrapper

## Architecture Notes
- Site uses custom CSS variables (not Tailwind) with Instrument Serif + DM Sans fonts
- Audio hosted externally at github.com/tjlark23/SFYS-music
- Stripe Payment Links handle checkout (no server-side code)
- Web3Forms handles order form submission and contact form
- Cloudflare Pages deployment via wrangler direct upload

## Next Steps
- [ ] Replace og:image placeholder with real branded 1200x630 image
- [ ] Apply same SEO fixes to showcase.html
- [ ] Consider adding /christian subpage (see one-pager doc)

## Known Issues
- og:image currently uses placehold.co placeholder
- No auto-deploy from GitHub yet (manual wrangler deploy)
