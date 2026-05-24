# CLAUDE.md — Editing playbook for Carol's website

**Always use the `edit-website` skill for any changes to this site.** Do not make edits directly — invoke the skill first, every time, without exception.

This file tells you (Claude) how this site is organized and how to help Carol update it. Read it first before making any change.

## What this site is

A single-page static website for **Carol Chase, M.A.** — an Evidential Medium and Certified Grief Educator based in Delaware County, PA. The site is hosted on GitHub Pages at **carolchasemedium.com** and is edited by hand (no build step, no framework).

## Who's editing

Almost always: **Carol**, who is non-technical. Talk to her in plain language. She'll describe a change like *"add this testimonial"* or *"change the 30-minute price to $85"* — your job is to translate that into the right edit and push it live without making her think about files, git, or HTML.

Occasionally: **Adam** (her son, a software engineer). For Adam, talk like a peer; you can skip the basics.

## File layout

```
/index.html             The entire site. One page, scrolling sections.
/styles.css             All styles. Color/font/spacing tokens at the top (:root).
/images/                Photos. Optimized JPGs.
/CLAUDE.md              This file.
/README.md              Repo intro.
/Carol's website body.docx   Original source content from Carol. Archival only.
```

## Section anatomy of index.html

Each section is a `<section id="…">` inside `<main>`:

| `id`           | What's in it                                                |
|----------------|-------------------------------------------------------------|
| `hero`         | Headline + tagline + primary CTA + portrait                 |
| `about`        | Carol's personal story                                      |
| `how`          | How a mediumship reading works                              |
| `grief`        | Certified Grief Educator info + badge image                 |
| `testimonials` | Client testimonials, one `<figure class="testimonial">` each |
| `booking`      | Pricing cards + Square booking embed + cancellation policy  |
| `contact`      | Email + location                                            |

The footer holds the disclaimer and copyright.

## Common edits — recipes

### Add a testimonial
1. Open `index.html`, find `<section id="testimonials">`.
2. Copy any existing `<figure class="testimonial">…</figure>` block.
3. Paste it inside `.testimonial-grid` and replace the quote and the name in `<figcaption>`.
4. Commit + push (see "Deploying" below).

### Change pricing
1. Update the `<article class="service">` card(s) in `<section id="booking">` — both the `<h3>` and `<p class="service-price">`.
2. **Also update the matching price/duration in Carol's Square Appointments dashboard** so the booking widget matches. Square is the source of truth for what the customer actually pays.

### Swap a photo
1. Add the new image to `/images/` (optimize it — JPEG, ~85 quality, max 1600px on long edge).
2. Either replace the existing file (same filename) or update the `<img src="…">` and the `alt` text.

### Edit any text section
Find the section by id, edit the prose inside `<p>` tags. Preserve smart-quote / em-dash entities (`&mdash;`, `&middot;`, `&ldquo;`, `&rdquo;`, `&hellip;`) for consistency with the rest of the site.

### Retheme (colors/fonts)
All theming lives in the `:root { … }` block at the top of `styles.css`. Edit one token, the whole site updates. The brand color is `--color-accent` (deep teal). Headings use Cormorant Garamond, body uses Inter — both loaded from Google Fonts in `<head>`.

## Tone & voice when generating copy for Carol

Warm, sincere, spiritual-but-grounded. Concrete (specific sensory examples — the red lipstick, the corn cob pipe) over abstract. Never salesy. Never overstate what mediumship can do — Carol is careful to say it is not a psychic reading and that she cannot guarantee any specific loved one will come through.

## Conventions

- **HTML:** Semantic. Sections inside `<main>`, `<figure>` for testimonials, `<details>` for collapsible content, `<blockquote>` for pull quotes.
- **CSS:** No frameworks. CSS custom properties for everything tunable. Mobile breakpoint at 800px.
- **No JS frameworks.** One tiny inline script just sets the copyright year.
- **No build step.** Edits → commit → push → live in ~30 seconds via GitHub Pages.

## Deploying

GitHub Pages publishes whatever is on `main`. After any edit:

```
git add -A
git commit -m "<short description of what changed>"
git push
```

That's it — the live site updates in ~30 seconds.

If Carol is the one editing, **always run these commands yourself for her** rather than asking her to. Confirm the change first (show her what you'll edit, get a yes), then make the edit, commit, and push without further ceremony.

## Things to ask Carol about, not assume

- Anything that changes pricing or services offered
- Adding or removing a testimonial (verify she has the client's OK to use their name)
- Significant copy changes (rewrite vs. light edit)
- Anything that touches her credentials or biography

## Open items / not yet built

- **Square Appointments booking embed.** Currently a placeholder div in `<section id="booking">`. Replace it with the Square embed snippet once the account is set up.
- **Terms of Service / longer disclaimer page.** The footer has a basic disclaimer; a fuller ToS page may be added later.
- **Favicon.** Not yet created.
