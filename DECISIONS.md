# Architecture Decisions

## 2026-03-10: SEO Backend Overhaul
- Applied SEO Bible V3 to existing site
- Kept all visual design, CSS, JS, audio, payments untouched
- Combined two separate JSON-LD scripts into single @graph
- Added Person schema for TJ Larkin (E-E-A-T)
- FAQ JSON-LD answers now match visible HTML text word-for-word
- Shortened title tag to under 60 chars per SEO Bible

## 2026-02-17: Initial Site Build
- Single-file HTML architecture (no framework)
- Cloudflare Pages for hosting (domain already on Cloudflare)
- Stripe Payment Links for checkout (no server needed)
- Web3Forms for form handling
- Audio hosted on separate GitHub repo (tjlark23/SFYS-music)
