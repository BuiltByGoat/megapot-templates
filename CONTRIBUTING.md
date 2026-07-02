# Contributing a template

One folder per template under `templates/<name>/`:

```
templates/<name>/
  index.html          # the template, with {{PLACEHOLDERS}} unfilled
  README.md           # audience, concept, section-by-section breakdown, screenshots
  screenshots/
    light.png         # hero, light scheme
    dark.png          # hero, dark scheme
    full-page.png     # full scrolled page (either scheme — whichever represents it best)
```

Templates are meant to be full scroll experiences, not a hero and a button — aim for 6+
substantive sections built from real, sourced content (Megapot's docs are the best source: odds
mechanics, prize structure, the money flow). See any existing template's README for the bar.

## Checklist (PRs are reviewed against this)

**Mechanics**
- [ ] Single self-contained HTML file — no external fonts, scripts, images, or CSS.
- [ ] Fills the full placeholder contract (see the root README): `{{SITE_NAME}}`, `{{TAGLINE}}`,
      `{{THEME_VARS}}` inside `:root{}`, `{{INVITE_URL}}` on every CTA, `{{DISCLAIMER}}` in the
      footer, `{{PAGE_NOTE}}` as a comment, `{{CLICK_BEACON}}` just before `</body>`.
- [ ] At least one element with `class="cta"` — long pages should repeat the CTA a few times
      down the scroll (the optional click beacon binds all of them).
- [ ] Light **and** dark palettes via `prefers-color-scheme`, plus
      `<meta name="color-scheme">`.
- [ ] Respects `prefers-reduced-motion` if you animate anything.
- [ ] No JavaScript. FAQs use native `<details>`/`<summary>`.

**Accessibility (WCAG 2.1 AA)**
- [ ] Text contrast ≥ 4.5:1 in both schemes (≥ 3:1 for large/bold display text).
- [ ] Visible `:focus-visible` ring on the CTA and every link.
- [ ] Tap targets ≥ 44px; `lang` attribute set.

**Honesty rules (non-negotiable — templates that break these won't merge)**
- [ ] Prize framing: "$1,000,000+ in daily prizes" / "daily prize pool". Never call the
      single jackpot $1,000,000 and never hardcode a jackpot figure.
- [ ] Attribute odds claims to Megapot ("Megapot's published odds"), don't assert them
      as the page's own guarantee.
- [ ] No earnings/income claims, no "guaranteed", no fake urgency (countdowns, "last
      chance"), no fabricated winners or testimonials.
- [ ] Keep the disclaimer slot and the independence note ("not affiliated with
      Megapot" ships in the default disclaimer text).
- [ ] Nothing aimed at minors.

## Testing

If you're working inside the megapot.build repo, embed the template and run the parity
test (`wizard/test-core.cjs`) — it asserts placeholder fill, beacon hook, light/dark
support, and the claims rules automatically.
