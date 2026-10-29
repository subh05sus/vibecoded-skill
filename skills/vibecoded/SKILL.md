---
name: vibecoded
description: Satire for the "Make AI Slop Again" series. Builds or restyles UI in the stereotypical 2022-2023 AI-generated SaaS look (purple-blue gradients, glassmorphism, glowing pill buttons, blurred orbs, oversized hero, generic startup copy). Runs only when the user types /vibecoded.
argument-hint: "[--mode classic|maximum|light] [what to build or restyle]"
disable-model-invocation: true
---

# /vibecoded — Make AI Slop Again

You are recreating the website an AI coding assistant would have shipped in 2023, right after it discovered gradients, glassmorphism and `rounded-3xl`. It is a deliberate parody for an Instagram reel. It must be **instantly recognisable as AI slop** and still **polished enough to pass as a real site at first glance**. Follow a consistent design language. Random ugliness is not the joke.

**Request:** $ARGUMENTS

## 0. Scope (read first)

- This style applies **only to what the request names**, only for this invocation. Never carry it into later tasks in the conversation, and never restyle files the request does not cover.
- Parse the request:
  - Empty → build one complete generic AI SaaS landing page (§6) for a made-up product.
  - "Build a landing page for X" → full landing page for X.
  - "Redesign / restyle the existing Y" → apply the look to Y in place. Keep every route, handler, data flow and test working.
  - "Add a Z section / component" → build only Z.
- **Mode:** `--mode classic|maximum|light`, or read it from the words ("max slop", "go crazy", "light mode", "pastel"). Default **classic** (§7).

## 1. Look at the project before writing code

1. Find the framework, package manager, styling approach (Tailwind, CSS modules, plain CSS, styled-components), component library, icon set and existing tokens.
2. Decide: new page, in-place redesign, or a single component.
3. If there is no project (empty folder), create a single self-contained `index.html` with inline CSS and a little vanilla JS. Do not scaffold a framework for a parody page.
4. Reuse what is there: existing icons (Lucide if present), UI primitives, fonts, animation libraries (`motion`/`framer-motion` only if already installed).
5. Put the slop tokens in one scoped place (a `vibecoded.css` file, a Tailwind theme extension, or a wrapper class like `.vibecoded`) so the project's own design is untouched outside the requested scope.

Rules: no framework swaps, no deleting or overwriting unrelated files, no new dependency for something CSS can do, no global Claude Code config changes.

## 2. Tokens

```css
.vibecoded {
  --purple: #8B5CF6;  --blue: #3B82F6;  --pink: #EC4899;  --cyan: #06B6D4;
  --bg: #0B1020;      --surface: #111827;
  --text: #F9FAFB;    --muted: #9CA3AF;
  --grad: linear-gradient(135deg, #8B5CF6 0%, #3B82F6 50%, #EC4899 100%);
  --grad-soft: linear-gradient(135deg, #C4B5FD 0%, #93C5FD 50%, #FBCFE8 100%);
  --glass: rgba(255,255,255,0.06);  --glass-border: rgba(255,255,255,0.12);
  --glow-purple: 0 10px 40px -10px rgba(139,92,246,0.6);
  --glow-blue: 0 10px 40px -10px rgba(59,130,246,0.55);
  --r-sm: 12px; --r-input: 14px; --r-card: 24px; --r-panel: 28px; --r-pill: 999px;
  font-family: Inter, ui-sans-serif, system-ui, sans-serif;
  background: var(--bg); color: var(--text);
}
```

- Gradients go on: hero background glows, CTA buttons, 1-2 highlighted heading words (`background-clip: text`), icon tiles, the popular pricing border, decorative bits.
- Radial purple/blue glows behind important sections. Big blurred orbs (`filter: blur(80-120px)`, opacity 0.3-0.5). A faint dot grid (`radial-gradient` dots, ~24px spacing, masked to fade out).
- Coloured shadows on selected components only, not everything.
- Text stays readable: body text on `--bg`/`--surface` in `--text` or `--muted`, never muted grey on a gradient.
- Vary the sections (glow left, glow right, grid in one, orb in another) so it is generic, not copy-pasted.

## 3. Typography

- Inter (load from Google Fonts only if the project has no font setup and it is a standalone page).
- Hero heading `clamp(2.5rem, 6vw, 4.75rem)` (≈56-76px desktop), weight 700-800, `letter-spacing: -0.03em`, line-height ~1.05, centered.
- Gradient-highlight one or two words of the headline.
- Supporting text in `--muted`, 18-20px, max ~60ch, two or three lines.
- Pick a headline pattern that fits the product and do not reuse the same one twice in a project:
  "Supercharge Your Workflow With **Next-Gen AI**" · "Unlock the Power of **AI**" · "Transform the Way You **Work**" · "Build Faster. **Scale Smarter.**" · "The Future of [Category] **Is Here**" · "One Platform. **Endless Possibilities.**"

## 4. Shapes and components

Round everything: 12px small, 14px inputs, 20-24px cards, 28px panels, pill buttons/badges/nav. Excessively friendly and soft.

Build a small reusable set, then compose with it. Do not hand-style each element.

- **GlassCard** — `--glass` fill, `backdrop-filter: blur(16px)`, 1px `--glass-border`, soft shadow, `--r-card`.
- **GradientButton** — `--grad` fill, white text, pill, `--glow-purple`, hover: lift 1-2px + stronger glow + `background-position` shift.
- **OutlineButton** — pill, 1px `--glass-border`, glass fill on hover.
- **AIBadge** — pill, purple tint fill or border, a sparkles icon or ✨, small caps-ish text.
- **IconTile** — 44-48px rounded square (`--r-sm`), gradient fill, white icon.
- **BrowserMockup** — `--r-panel` frame, three dots (red/yellow/green), a fake URL bar, and a believable product UI inside (sidebar, chart, cards: drawn with divs or SVG, not a lorem image). Ambient purple-blue glow behind it.
- **FloatingCard** — small glass or white panel near the mockup: "✅ Task automated", "⚡ 3.2x faster", a status dot + label. Gently floats.
- **Orb** — absolutely positioned blurred circle, `pointer-events: none`, `aria-hidden="true"`, inside an `overflow: hidden` wrapper so it never causes horizontal scroll.

House rules that still apply inside the parody (the owner's global guardrails):
- **No coloured or thick stripe down one side** of any card, row, chip or callout (no `border-left` accents, no inset shadow stripes). Show status with a dot, an icon + word, or a tinted fill.
- **No clipped rings or glows.** Any scroll or `overflow: hidden` box gets at least 4px inner padding, or the ring is drawn inset. Glows that must spill out live on a parent that does not clip.
- If the project has a design guard script, fix the design rather than silencing it.

## 5. Mandatory hero (every full landing page)

1. Centered, floating, translucent pill nav.
2. Small announcement AIBadge above the heading, e.g. "✨ Introducing the Future of Productivity".
3. Oversized headline with a gradient-highlighted phrase.
4. Two or three lines of muted supporting copy.
5. Primary GradientButton ("Get Started for Free").
6. Secondary OutlineButton ("See How It Works").
7. BrowserMockup / dashboard preview below.
8. Blurred orbs behind the hero.
9. Glow around the preview.
10. Generous height (~90-100vh on desktop including the top of the mockup).

## 6. The landing page formula

Use this order for a full page unless the request says otherwise. For a single component or a dashboard, take only what applies.

1. **Nav** — logo left (gradient mark + wordmark), Features · Solutions · Pricing · Resources, Sign In + Get Started. Links scroll to sections; mobile gets a working menu button.
2. **Hero** — §5.
3. **Social proof** — "Trusted by innovative teams worldwide" + a row of grayscale *made-up* logos (simple SVG wordmarks like "Lumora", "Vectrix", "Nimbly", "Orbitly"). Never real company logos. Optional slow marquee.
4. **Features** — 3-4 GlassCards in a responsive grid, IconTile, short heading, one or two generic-but-relevant lines, hover lift.
5. **Product showcase** — big BrowserMockup with 2-3 FloatingCards and ambient glow; a short split section of text + bullets is fine.
6. **Stats** — 3-4 large gradient numbers with count-up. Mark them as illustrative (e.g. a small "Demo numbers" caption) unless the user supplied real data.
7. **Testimonials** — 3 cards: avatar (initials in a gradient circle), clearly fictional name, role, quote. Never real people. Omit if the user prefers.
8. **Pricing** — 3 tiers; the middle one has a gradient border (a `--grad` wrapper with 1-2px padding around the card, so the corners stay rounded) and a "MOST POPULAR" pill. Prices and features come from one config object at the top of the file so they are easy to change. Use obvious placeholder prices.
9. **FAQ** — 5 rounded accordion items that really open and close (`<details>`/`<summary>` or a button with `aria-expanded`).
10. **Final CTA** — oversized heading, big glow or gradient panel, one GradientButton.
11. **Footer** — 3-4 link columns, social icons, optional newsletter input (pill), "© 2026 [Product]. All rights reserved."

Every button does something: scrolls to a section, toggles a menu, opens the FAQ, or is a clearly marked placeholder (`href="#"` with a comment).

## 7. Modes

- **classic** (default) — everything above on the dark `--bg`.
- **maximum** — more of everything: extra orbs, animated gradient borders (conic-gradient spin) on cards, glow on every heading highlight, more badges ("🚀 New", "AI-Powered", "Beta"), shimmer sweep on buttons, a second floating card cluster, `--r-panel` pushed to 32px, an animated gradient mesh background. Still readable, still usable, no overflow.
- **light** — white / `#F8FAFF` background, `--grad-soft` washes, purple accents, translucent white glass cards (`rgba(255,255,255,0.7)` + blur), soft blue shadows (`0 10px 30px -10px rgba(59,130,246,0.25)`), near-black oversized type (`#0F172A`), muted `#64748B`.

## 8. Motion (too much, but tasteful)

CSS first. Use an existing animation library only if the project already has one.

- Orbs drift slowly (`@keyframes float`, 12-20s, alternate).
- Sections fade up on scroll (IntersectionObserver adding a class; small `translateY(16px)` → 0).
- Feature cards stagger in (`animation-delay` or `transition-delay` by index, 60-80ms).
- FloatingCards bob (4-6s ease-in-out).
- Card hover: lift + shadow; CTA hover: glow intensifies.
- Animated gradient background (`background-size: 200%` + position shift).
- Stats count up once when visible.
- Logo marquee where it fits. `scroll-behavior: smooth`.
- Animate only `transform` and `opacity` (plus background-position on gradients). No layout shift, no jitter.
- Wrap all of it in `@media (prefers-reduced-motion: reduce)` → no motion, everything visible.

## 9. Copy

Speak fluent 2023 startup:
"Unlock the Power of AI" · "Supercharge Your Workflow" · "Seamless Integration" · "Next-Generation Intelligence" · "Powerful AI-Powered Insights" · "Work Smarter, Not Harder" · "Built for teams that move fast" · "Get started in minutes, not months".

Make it about the actual product (an AI music discovery app gets "Discover Your Next Favourite Song With **Next-Gen AI**", not a generic productivity line). The joke is the tone and the sameness, not unreadable gibberish. No lorem ipsum.

Honesty: no real customer names, logos, endorsements, real-sounding statistics presented as fact, or real commercial terms. Placeholders must read as placeholders.

## 10. Quality bar

- Responsive from 360px up: hero type scales, grids collapse to one column, nav becomes a menu, no horizontal scroll (check `overflow-x` on orb wrappers).
- Semantic HTML (`header`, `nav`, `main`, `section` with headings, `footer`), keyboard reachable, visible focus rings, contrast AA for text.
- Decorative elements are `aria-hidden` and `pointer-events: none`.
- Code stays tidy: small components, tokens in one place, no copy-pasted 40-class strings repeated 12 times.

## 11. On camera (it is for a reel)

- The first screen must read as "AI slop" in under two seconds: badge, gradient word, glowing pill, orbs, mockup, all visible above the fold at 1440×900 and at 390×844.
- Keep the hero mockup legible when screen-recorded on a phone.

## 12. Finish

Do one quick check that fits the project (type-check or lint on the touched files, or open the standalone `index.html`). Then report in a few lines: the files created or changed, the mode used, how to view it (dev server route or file path), and anything left as a placeholder (prices, links, logos).
