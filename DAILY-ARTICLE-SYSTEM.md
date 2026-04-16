# Songs For Your Story — Daily Article System

Single source of truth for writing and publishing articles on songsforyourstory.com. Any automated Claude Code session that opens this repo at 6:30 AM CT reads this file first and follows it exactly.

---

## 1. Rotation

**Five articles per week, Monday through Friday.** Saturday, Sunday: no new articles.

| Day | Pillar | Category tag class |
|-----|--------|---------------------|
| Monday | Pillar 1 · Life Events & Celebrations | `tag-graduation` / `tag-birthday` / contextual |
| Tuesday | Pillar 2 · Relationships & People | contextual (coral/purple/sage) |
| Wednesday | Pillar 3 · Business & Professional | `tag-business` |
| Thursday | Pillar 4 · How-To & Creative | `tag-graduation` / contextual |
| Friday | Pillar 5 · Seasonal & Trending | seasonal (coral for Mother's/Father's Day, etc.) |

If the script runs on Sat/Sun for any reason, exit without writing.

---

## 2. Topic selection

1. Open `content-queue/topics.md`.
2. Determine today's day of week → pillar.
3. Pick the **first** unchecked `[ ]` item under today's pillar heading.
4. If that pillar has no unchecked items, fall through to the next pillar in rotation (Pillar 2 → 3 → 4 → 5 → 1).
5. After the article is published successfully, change `[ ]` to `[x]` on that line and append ` — YYYY-MM-DD`.
6. If the queue has fewer than 3 unchecked items in the selected pillar, append a note at the end of the file: `REFILL NEEDED: pillar <N>`.

---

## 3. Voice rules

- **First person.** TJ Larkin is the author. "I" and "we" are fine. "Songs For Your Story" used as the business.
- **Direct, conversational, confident.** Short paragraphs (1–3 sentences). Warm, specific, 8th-grade reading level.
- **Lead with specifics.** Real prices ($49 / $149 / $199), real moments, real people. No vague "meaningful gift" language.
- **Open with a scenario or concrete claim**, not a definition or a general observation. The first dance. The graduation hug. The party that went silent.
- **SFYS product anchors:** mention the $49 starting price or the $149 wedding tier in every article where a pricing anchor fits.

### Zero em-dashes

Never use `—` (em dash). Use periods or commas. Run `grep "—" articles/<slug>.html` before commit.

### Zero slop words

Banned list (case-insensitive, whole-word match):

`delve`, `crucial`, `landscape`, `leverage`, `harness`, `unlock`, `navigate`, `seamless`, `robust`, `cutting-edge`, `game-changer`, `utilize`, `foster`, `empower`, `elevate`, `embark`, `realm`, `tapestry`

Scan the finished article body before commit. If any slop word is found, rewrite that sentence.

---

## 4. Article specs

- **Length:** 1000–1400 words in the body (exclude nav/footer/schema). Longer than WilCo because SFYS articles convert to $99–$199 custom song sales, so we need room to carry the reader through the story.
- **Exactly one `<h1>`** (the article title).
- **4–6 `<h2>` section headings** in the body.
- **FAQ block** with exactly 3 Q/A pairs matching the on-page FAQ accordion.
- **At least one internal link** to the relevant occasion landing page or pricing anchor. Primary targets:
  - `https://songsforyourstory.com/#pricing` (general pricing)
  - `https://songsforyourstory.com/graduation.html#pricing` (graduation articles)
  - `https://songsforyourstory.com/christian` (faith-adjacent)
  - Another article from `/articles/` that relates to the topic
- **At least two internal links total** — the occasion page plus one cross-article link.
- **Date:** today's date in ISO (`2026-04-16`) and human format (`April 16, 2026`).
- **CTA copy:** every article's closing CTA section should say: `Order your custom song at songsforyourstory.com/order or email tj@songsforyourstory.com`. Note: `/order` is TJ's canonical CTA phrasing. Until that route exists, the button link itself points at `https://songsforyourstory.com/#pricing` (or the relevant occasion-page pricing anchor). The text copy still reads "Order your custom song at songsforyourstory.com/order" so brand messaging stays consistent.

---

## 5. SEO requirements (hard gate)

Every article must pass:

1. **Title tag** unique, 50–72 characters, ends with `| Songs For Your Story`.
2. **Meta description** 140–160 characters, no duplication of another page's description.
3. **Canonical** `<link rel="canonical">` pointing to the full URL (no `.html`, matches Cloudflare Pages stripping): `https://songsforyourstory.com/articles/<slug>`.
4. **Open Graph** `og:title`, `og:description`, `og:type="article"`, `og:url`, `og:image`, `og:site_name`. Use `og-graduation.png` for graduation pieces, `og-main.png` otherwise.
5. **Twitter card** `twitter:card="summary_large_image"`.
6. **JSON-LD (four blocks inside `@graph`, valid JSON):**
   - `Organization` (Songs For Your Story) with `@id` anchor.
   - `Person` (TJ Larkin founder) with `@id` anchor.
   - `Article` with `headline`, `author` (@id ref), `publisher` (@id ref), `datePublished`, `dateModified`, `mainEntityOfPage`, `image` when available.
   - `FAQPage` with exactly 3 `Question`/`Answer` pairs that mirror the on-page FAQ accordion.
   - (The existing SFYS template uses Organization + Person + Article + FAQPage. BreadcrumbList is allowed and encouraged — add it as a fifth node if easy.)
7. **Exactly one `<h1>`** in the rendered HTML.
8. **robots.txt and sitemap.xml still resolve 200** after the sitemap update.

---

## 6. HTML template

Use `articles/custom-wedding-songs.html` as the exact template. SFYS articles are flat files in `/articles/<slug>.html` — not subdirectories.

**Copy verbatim** from that file:
- Full `<head>` shell (viewport, fonts, CSS `<style>` block, Meta Pixel script)
- `<header><nav class="nav">…</nav></header>` navigation
- `<footer>` element and footer markup
- `article-hero` structure
- `article-body` wrapper with `article-cta` and `faq-section` classes
- FAQ accordion markup (`.faq-item` / `.faq-q` / `.faq-a`)

**Replace for the new article:**
- `<title>`, `<meta name="description">`, `<meta name="keywords">`, canonical, all OG/Twitter tags
- JSON-LD `@graph` block (new headline, datePublished, dateModified, 3 FAQ Q/A pairs that match on-page)
- Hero section (`article-hero`): category label color and text, `<h1>`, subtitle, meta line (`By TJ Larkin · <date> · <N> min read`)
- Body: all paragraphs and H2 sections (1000–1400 words)
- FAQ section: 3 new Q/A pairs, matching the JSON-LD exactly
- Final `article-cta` block copy + button link

---

## 7. Quality check (before commit)

```
# 1. Em-dash scan
grep "—" articles/<slug>.html                 → expect 0

# 2. Slop scan
for word in [delve, crucial, landscape, leverage, harness, unlock,
             navigate, seamless, robust, cutting-edge, game-changer,
             utilize, foster, empower, elevate, embark, realm, tapestry]:
    grep -iw "$word" articles/<slug>.html     → expect 0

# 3. JSON-LD valid
python3 -c "import json, re; html=open('articles/<slug>.html').read();
            m=re.search(r'<script type=\"application/ld\\+json\">(.*?)</script>', html, re.DOTALL);
            print(json.loads(m.group(1)))"    → expect no errors

# 4. H1 count
grep -c "<h1" articles/<slug>.html            → expect 1

# 5. Word count of body
python3 -c "import re; h=open('articles/<slug>.html').read();
            art=re.search(r'<article class=\"article-body\">(.*?)</article>', h, re.DOTALL).group(1);
            txt=re.sub(r'<[^>]+>', ' ', art);
            print(len(re.sub(r'\\s+',' ',txt).split()))"
                                               → expect 1000–1400

# 6. Internal link count
grep -c 'href="https://songsforyourstory.com' articles/<slug>.html   → expect >= 2
grep -c 'href="/articles/' articles/<slug>.html                       → expect >= 1 (cross-article)
```

If any check fails, stop, fix the article, re-check. Do not commit a failing article.

---

## 8. Publish flow (the 5 steps)

1. **Save article** → `articles/<slug>.html` (slug is kebab-case, lowercase, matches the queued topic's slug).
2. **Update `/articles/index.html`** → insert a new `<a class="article-card">` block **at the top of the cards grid** (above the currently-first card). Use the exact card pattern from existing entries. Required elements: category `<span class="article-card-tag">` with the right tag class, `<h2 class="article-card-title">`, `<p class="article-card-desc">` (2-line excerpt), `<div class="article-card-meta">` (`N min read · <Month Year>`).
3. **Update `/sitemap.xml`** → add a `<url>` block for the new article with `<loc>https://songsforyourstory.com/articles/<slug></loc>`, `<lastmod>` = today, `<changefreq>monthly</changefreq>`, `<priority>0.7</priority>`.
4. **Update `content-queue/topics.md`** → mark the topic `[x]` with today's date appended.
5. **Append to `automation/daily-log.md`** → new line at the top of the log list in the documented format. Commit SHA filled after commit.

**Commit:** `article: <slug> (<pillar name>)`
**Push:** `git push origin main`

Cloudflare Pages auto-deploys from `main`. Verify live within 90 seconds by curl-ing `https://songsforyourstory.com/articles/<slug>` for HTTP 200.

---

## 9. If anything fails

- **Slop/em-dash fails:** rewrite, rerun checks, do not commit.
- **JSON-LD invalid:** fix JSON, do not commit.
- **Cloudflare deploy 404:** wait 90 seconds, curl again. If still 404, flag the commit hash in `automation/daily-log.md` with `DEPLOY FAILED` and stop.
- **Topic queue empty for today's pillar and next one:** flag `REFILL NEEDED: pillar <N>` at the bottom of `topics.md` and stop. Do not invent a topic on the fly.
- **Nothing else. No other "creative" handling.** If the spec above does not cover the failure, stop and leave the repo in a clean state for a human to review.

---

## 10. File paths cheat sheet

```
content-queue/topics.md                     ← queue, source of truth
automation/daily-log.md                     ← human-readable publish journal
automation/daily-log.txt                    ← runtime stdout/stderr from launchd
DAILY-ARTICLE-SYSTEM.md                     ← this file
articles/<slug>.html                        ← new article lives here (FLAT, not nested)
articles/index.html                         ← article list, prepend new card
articles/custom-wedding-songs.html          ← template
sitemap.xml                                 ← SEO discovery
```

---

## 11. DRY_RUN behavior

If the environment variable `DRY_RUN=1` is set when this script runs, the session must NOT write an article, NOT touch git, NOT modify any files. Instead, echo a single line to stdout:

```
Hermes dry run OK — would have written <pillar name> article
```

Then exit cleanly. This is used by launchd kickstart tests so we can fire the plist without burning through a topic.

---

*Last updated: 2026-04-16. When this file changes, bump the date.*
