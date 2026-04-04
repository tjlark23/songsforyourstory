# Project Status

## Last Updated: 2026-04-04
## Repo: https://github.com/tjlark23/songsforyourstory
## Live URL: https://songsforyourstory.com
## Stack: Static HTML/CSS/JS, Cloudflare Pages

## Current State
- Working: Full site live with audio players, Stripe payments, Web3Forms contact/order forms
- Working: SEO optimized per SEO Bible (canonical, OG tags, Twitter Card, JSON-LD @graph, semantic HTML, aria-labels)
- Working: robots.txt and sitemap.xml
- NEW: graduation.html landing page with all 5 demo songs wired up, ready for Stripe links + deploy

## Last Session (2026-04-04)
- Built graduation.html landing page for /graduation funnel
- Graduation-specific pricing: The Milestone ($49), The Legacy ($149), The Send-Off ($199) with 50% off anchor pricing
- Graduation-specific order form with school, next step, graduation date fields
- Full SEO: JSON-LD with FAQPage schema, OG tags, canonical URL, semantic HTML
- Design matches main site with purple graduation accent, early adopter urgency framing
- Featured Connor demo card + compact playlist with 4 new graduation songs (Emma/country, Jaylen/hip-hop, Friends/indie-folk, Marcus/pop-rock)
- All 5 songs wired to SFYS-music repo Graduation folder with correct durations
- Updated sitemap.xml to include /graduation
- Stripe payment links still need to be created and inserted (search for PLACEHOLDER in graduation.html)

## Previous Session (2026-03-10)
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
- [ ] TJ: Create 3 Stripe payment links ($49, $149, $199) and replace PLACEHOLDER URLs in graduation.html
- [ ] Deploy all files to Cloudflare Pages (graduation.html + updated sitemap.xml)
- [ ] Add "Graduation Songs" link to main site nav (index.html)
- [ ] Replace og:image placeholders with real branded 1200x630 images
- [ ] Set up Meta ads campaign for graduation page
- [ ] Apply same SEO fixes to showcase.html
- [ ] Consider adding /christian subpage (see one-pager doc)

## Known Issues
- og:image currently uses placehold.co placeholder
- No auto-deploy from GitHub yet (manual wrangler deploy)
