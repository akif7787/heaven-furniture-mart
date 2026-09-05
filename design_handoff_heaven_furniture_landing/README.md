# Handoff: Heaven Furniture Mart — Bespoke Furniture Landing Page

## Overview

A premium editorial landing page for **Heaven Furniture Mart** — a bespoke luxury furniture atelier based in Agrabad, Chattogram, Bangladesh. The design targets a single conversion goal (**Request a Custom Quote**, routed through WhatsApp) and communicates quiet-luxury, bespoke craftsmanship, and a physical showroom presence through image-led storytelling.

Not e‑commerce. Not a SaaS site. This is a **lead-generation landing page** with one clear CTA repeated throughout.

## About the Design Files

The files in this bundle are **design references created in HTML** — they are prototypes showing intended look, motion, and behavior. They are **not production code to copy directly**.

The task is to **recreate the design in the target codebase's existing environment** (React, Vue, Next.js, Astro, SvelteKit, native, etc.) using its established patterns and libraries. If no codebase exists yet, use the framework best suited to a marketing site — **Next.js (App Router) or Astro** are both excellent fits since the page is largely static + light JS. The current HTML uses vanilla JS + CSS custom properties, so porting to any framework is straightforward.

## Fidelity

**High-fidelity (hifi).** All colors, typography, spacing, layouts, imagery, animations, and copy are final and production-ready. Recreate pixel-for-pixel using the codebase's chosen framework. The prototype uses Google Fonts (Cormorant Garamond + Inter) and CSS custom properties — those tokens should map cleanly into whatever design-token system the target project uses (Tailwind config, CSS variables, MUI theme, etc.).

## Screens / Views

This is a **single-page landing** composed of one continuous scroll experience with a fixed header, a preloader intro, and eleven visual sections. Section order matters — it drives the reading path: **Brand → People → Collections → Bespoke → Trust → Showroom → Story → CTA**.

### 0. Preloader (Page Entry Intro)

- **Purpose**: A 1.2–1.8s premium editorial intro. Not a loading screen — the page is already interactive underneath.
- **Layout**: Full-viewport fixed overlay, dark charcoal-teal background, everything centered.
- **Sequence** (durations for desktop; multiply by ~0.75 for mobile):
  1. **0–80ms**: Overlay is solid `#1a2420`, logo hidden.
  2. **80ms**: Logo fades in from `opacity: 0; scale(0.96); filter: blur(10px)` → `opacity: 1; scale(1); filter: blur(0)` over 900ms.
  3. **620ms**: A thin brass line (`#b89661`, 1px height, ~180px wide) draws horizontally from width 0 → full over 900ms.
  4. **980ms**: `"DESIGNED · CRAFTED · CUSTOMIZED"` uppercase text (10.5px, 0.34em letter-spacing, 0.72 white) fades in with a 6px upward translate over 600ms. Dot separators are brass-colored at 0.4 opacity.
  5. **1450ms**: The whole overlay lifts up (`translateY(-100%)`) over 1.2s with the inner content quickly fading. Simultaneously the hero image reveals through a `clip-path` mask that opens top→bottom (`inset(0 0 100% 0)` → `inset(0 0 0 0)`) over 1.4s.
  6. **2000ms**: Preloader is removed from the tree; body scroll unlocks (`body.preloading` class removed).
- **Assets**: `assets/heaven-logo.jpg` (480×480 full logo tile — dark teal chip with white "HEAVEN" wordmark + brass "A" + white "FURNITURE MART" subtitle).
- **Reduced motion**: Skip all timings to <100ms and just cross-fade.

### 1. Header (Fixed Navigation)

- **Purpose**: Persistent global navigation with the brand logo and the primary CTA.
- **Position**: `position: fixed; top: 0; left: 0; right: 0; z-index: 100;`
- **Two states**:
  - **Transparent (over hero, `scrollY ≤ 40`)**: No background, color inherits to `--ivory (#f4efe6)`. Padding 24px vertical desktop / 18px mobile. Min-height 76px / 68px.
  - **Scrolled (`scrollY > 40`)**: Background `rgba(244,239,230,0.86)` with `backdrop-filter: saturate(1.2) blur(14px)`. Bottom border 1px `rgba(26,36,32,0.14)`. Color switches to `--ink (#1a2420)`. Padding 14px vertical desktop / 12px mobile. Min-height 60px / 56px. Transition all properties 0.55s `cubic-bezier(0.4, 0, 0.2, 1)`.
- **Layout**: Flex row, `justify-content: space-between; align-items: center; gap: 24px`.
- **Left — Brand logo**: `<a href="#top">` containing the tight-cropped logo image (`assets/heaven-logo-tight.jpg`, 280×130px source). Displayed at `height: 36px` desktop / `30px` mobile — width auto. `border-radius: 3px`. Subtle box-shadow `0 8px 24px rgba(0,0,0,0.12)`. Hover: `translateY(-1px)` transform over 0.5s.
- **Center — Nav links**: (hidden on mobile) `Collections · Bespoke · Our Story · Showroom`. Inter font, 11.5px, letter-spacing 0.24em, uppercase, weight 500, opacity 0.9. Gap 44px. Underline animation on hover — a 1px pseudo-element line under the link that scales from `scaleX(0)` to `scaleX(1)` from the left over 0.5s.
- **Right — CTA**: Pill button `"Request a Custom Quote →"`. Inter 10.5px 500 weight, 0.22em letter-spacing, uppercase. Padding 12px 20px. Border 1px currentColor. Border-radius 999px. Arrow `→` shifts `translateX(6px)` on hover. On transparent state hover flips background to ivory / text to ink. Hidden on mobile.
- **Mobile — Hamburger**: 36×36px button, two 1px horizontal lines at top 14px and bottom 14px. Animates to an X on `.mobile-open` state.
- **Mobile menu overlay** (when hamburger tapped): `position: fixed; inset: 0; z-index: 99` panel that slides down from `translateY(-100%)` to `0` over 0.6s. Ivory background, large serif nav links (`clamp(40px, 9vw, 64px)` Cormorant Garamond), phone/email/address at bottom.

### 2. Hero (Section, ~100vh)

- **Purpose**: Cinematic opening statement — the moment the visitor forms an impression.
- **Layout**: `min-height: max(100svh, 720px)`. Flex column. Content is layered on top of a full-bleed background image (dark charcoal fallback).
- **Structure** (top to bottom inside hero):
  - **Background image** (`assets/hero.jpg`, ~2560×1920, warm minimal interior — brown sofa, woven chairs, iron stove, stacked firewood). `position: absolute; inset: 0`. Object-fit cover. On load: `scale(1.06)` → `scale(1)` over 1.8s. Gradient overlay: `linear-gradient(180deg, rgba(15,20,18,0.55) 0%, rgba(15,20,18,0.15) 30% / 55%, rgba(15,20,18,0.75) 100%)` for text legibility.
  - **hero-top rail**: Padded `140px top desktop / 116px tablet / 108px mobile`, sides `--pad`. Two mono labels (11px, 0.22em letter-spacing, uppercase, Inter 500). Left: `"Agrabad · Chattogram / Bangladesh"`. Right (aligned right): `"Est. 2020 / Bespoke Atelier"`. Second line at 65% opacity.
  - **hero-body** (pushed to bottom via `margin-top: auto`): 2-column grid `1fr auto`, gap 48px, align-items end. Padded sides `--pad`, bottom `clamp(48px, 8vh, 96px)`. Contains:
    - **Headline** (`h1.hero-headline.h-display`): `Cormorant Garamond` 400 weight, `clamp(56px, 10vw, 168px)`, line-height 0.94, letter-spacing -0.02em. Three lines: `"Furniture,"` / `"crafted"` / `"around <em>you</em>."` — the italic `you` is in brass `#b89661`. Each line is a `<span class="line"><span>...</span></span>` — outer clips, inner translates from `translateY(110%)` to `0` over 1.1s with 0.15s stagger between lines.
    - **hero-right column** (max-width 320px, right-aligned): Supporting paragraph `"Bespoke furniture designed around your space, your taste, and the way you live."` (15px, 1.55 line-height, 82% ivory). Below it, the primary CTA: `"Request a Custom Quote →"` — outlined pill in ivory on the dark hero, flips to solid ivory-bg / ink-text on hover.
  - **hero-bottom bar**: Border-top `1px rgba(244,239,230,0.15)`, margin-top 32px, padding 22px top / 28px bottom. Flex row space-between. Left: mono tagline `"Designed · Crafted · Customized"`. Right: `"Scroll to explore"` mono label + a 1px×32px vertical bar animating a brass fill up→down infinitely over 2.4s.

### 3. Section 01 / The People

- **Purpose**: Introduce the real Managing Director and team via an editorial composition — this is the "human" moment before the product moments.
- **Background**: `--paper (#f8f5ee)`, warmer/slightly darker than the base ivory.
- **Padding**: `--pad-y` vertical (`clamp(80px, 12vh, 160px)`), `--pad` sides.
- **Layout**: 12-col-style asymmetric grid: `grid-template-columns: 5fr 7fr; gap: clamp(40px, 6vw, 96px); align-items: center`.
- **Left column (5fr)**:
  - Section label: `<span class="rule"></span>01 / The People` — a 32×1px brass line beside 11px 0.24em uppercase Inter 500 in brass `#a88547`.
  - Headline: `"A belief in"` / `"crafted<em>manship</em>."` italic `craftsmanship` in brass. Cormorant Garamond `clamp(44px, 6.8vw, 112px)`, 0.98 line-height, -0.015em letter-spacing.
  - Lede quote (italic Cormorant 20–28px, 1.4 line-height): `"At Heaven Furniture Mart, we believe furniture is more than function; it is a reflection of lifestyle, taste, and comfort. Every piece we create is designed to bring lasting elegance into the homes of our clients."`
  - Attribution block (top-border 1px `--line`, max-width 400px, padding-top 24px): Italic Cormorant 24px `"Abul Kalam Bhuiyan"` above uppercase 11px 0.22em 500 `--muted` `"Managing Director · Founder"`.
- **Right column (7fr)** — `<figure class="people-right reveal-img">`:
  - **Photo container** (`.people-photo`): `aspect-ratio: 5/4`, `overflow: hidden`. Object-fit cover, `object-position: center 40%` (keeps the MD's face in frame while showing the seated pose). Image is `assets/md-team.jpg` — the real photograph of the MD (older gentleman in gray suit, seated on a royal blue tufted sofa) with 5 team members standing behind him at what appears to be a trade fair booth.
  - **Caption below the photo**: 20px margin-top, 1px brass left border, 16px left padding. Two lines: uppercase 10.5px 0.22em brass `"Photographed at"` above italic Cormorant 16px muted `"International Furniture Fair, Chattogram · 2024–25"`.
- **Reveal animation**: The image container has `.reveal-img` — clip-path masks from `inset(0 0 100% 0)` to `inset(0 0 0 0)` over 1.4s, inner img scales from 1.10 → 1.00 over 1.8s. Text elements use `.reveal` with `translateY(32px)` + opacity, staggered `.reveal-delay-1/2/3` (100ms / 220ms / 340ms).
- **Mobile**: Grid collapses to single column, image aspect becomes 4/3.

### 4. Section 02 / Collections

- **Purpose**: Present four furniture categories as image-led editorial chapters (NOT a card grid). Each is one full-width horizontal block with alternating image/text orientation.
- **Background**: `--ivory (#f4efe6)`.
- **Section header**:
  - Grid `1fr 1.6fr`, gap `clamp(24px, 4vw, 80px)`, margin-bottom `clamp(48px, 8vw, 96px)`.
  - Left: section-num label `"02 / Collections"`.
  - Right: h2 `"Spaces,"` / `<em>"shaped beautifully."</em>` — same h-1 scale as section 01.
- **Each collection article**: `padding: clamp(48px, 8vw, 96px) 0; border-top: 1px solid var(--line)`. Last one adds `border-bottom`. Grid `6fr 6fr`, gap `clamp(32px, 5vw, 80px)`, `align-items: center`.
- **Alternation** (`.reverse` class flips the image to the right):
  - **01 Living** — image left, text right. Image `assets/living.jpg`. Categories: `Sofas · Coffee Tables · TV Units · Consoles`. Description: `"Anchor pieces designed for the rooms where life gathers — proportioned to your space, upholstered to your touch."`
  - **02 Bedroom** — image right (reverse), text left. Image `assets/bedroom.jpg`. `Beds · Wardrobes · Dressing Tables · Bedside Tables`. `"Quiet rooms deserve considered pieces. Built to your dimensions, finished in the wood and tone that suit your home."`
  - **03 Dining** — image left. `assets/dining.jpg`. `Dining Tables · Dining Chairs · Cabinets`. `"A dining room is a stage for the people you love. Solid timber, honest joinery, and seating shaped for long evenings."`
  - **04 Office & Study** — image right (reverse). `assets/office.jpg`. `Executive Tables · Bookshelves · Workstations`. `"Rooms for focus. Executive desks, considered bookshelves and workstations — proportioned around how you actually work."`
- **Image container** (`.col-image`): `aspect-ratio: 4/5` (portrait), `overflow: hidden`. Has `.reveal-img` for clip-path masked reveal. On article hover: image scales `1 → 1.04` over 1.4s.
- **Body column** (`.col-body`): Flex column, gap 24px.
  - **Index** (`.col-index`): Cormorant italic 300 weight, `clamp(64px, 8vw, 120px)`, brass color. Just the number ("01", "02"…).
  - **Title** (`.col-title` h3): Cormorant 400, `clamp(40px, 5vw, 72px)`, line-height 1, -0.01em tracking.
  - **Item list** (`ul.col-items`): Flat inline list, no bullets. Items separated by a brass `·` dot. 13px, 0.06em letter-spacing, `--muted` color.
  - **Description** (`.col-desc`): 15.5px, 1.6 line-height, `rgba(26,36,32,0.72)`, max-width 42ch.
  - **CTA link** (`.col-cta`): Uppercase Inter 500 11px 0.24em `"Request a Custom Quote →"`. A 24px brass line sits below it (`::before`) — on article hover this line grows to `100%` width over 0.5s. Arrow shifts `translateX(6px)` on hover.
- **All collection CTAs route to the same WhatsApp deep-link** (see WhatsApp section below). Do not use "Enquire", "Shop", or "Buy Now" — every CTA uses the same "Request a Custom Quote" label.
- **Mobile**: Single-column stack, `.reverse` order neutralized so image always sits above text.

### 5. Section 03 / Bespoke (Dark)

- **Purpose**: The core differentiator moment — custom-made furniture. Strongest visual weight on the page.
- **Background**: `--ink (#1a2420)`, color `--ivory`.
- **Padding**: `--pad-y` vertical.
- **Section header**: Same grid pattern. Label `"03 / Bespoke"`. Headline: three lines `"Your space."` / `"Your dimensions."` / `<em>"Your piece."</em>` — italic third line in brass `#b89661`.
- **bespoke-stage** — the visual set-piece:
  - **Wide image** (`.bespoke-wide`): `aspect-ratio: 21/9`, cinematic. Image `assets/bespoke-wide.jpg` (walnut wood interior). Has `.reveal-img` for masked reveal.
  - **Inset detail image** (`.bespoke-inset`): `position: absolute; right: clamp(24px, 5vw, 64px); bottom: -70px`. Size `clamp(180px, 22vw, 340px)` square. `border: 8px solid var(--ink)` creates a visible frame separation. Deep shadow `0 30px 80px rgba(0,0,0,0.5)`. Image `assets/wood-detail.jpg` (wood grain close-up). Reveals with `.reveal-img.reveal-delay-2` (240ms later than the wide image).
- **Lede paragraph** (after the images, `margin-top: 40px`): Italic Cormorant `"Fully bespoke furniture, built around your space — not mass-produced. Every commission begins with a conversation and ends with a piece that could only belong to your home."` Max-width 640px, `rgba(244,239,230,0.85)`.
- **Process row** (`.process`, `margin-top: clamp(120px, 15vh, 180px)`): 4-column grid on desktop, 2-col at ≤960px, 1-col at ≤560px. Border-top 1px `--line-dark`. Padding-top 56px. Each `.process-step` is a flex column, gap 20px, with:
  - Italic Cormorant number (`.num`, 300 weight, `clamp(56px, 6vw, 88px)`, brass color).
  - Uppercase 12px 0.28em title.
  - 14px muted description max 22ch wide.
  - Content:
    - `01 CONSULTATION` — "A free conversation about your space, needs, and taste."
    - `02 DESIGN` — "Concepts, materials and dimensions, tailored to your home."
    - `03 CRAFT` — "Built with skilled in-house craftsmanship at every stage."
    - `04 DELIVERY + INSTALL` — "We bring the piece to you, and place it, ourselves."
  - Each step uses `.reveal-delay-N` for sequential reveal.
- **Bespoke section CTA** (`margin-top: clamp(64px, 8vw, 96px)`): Flex row space-between, wraps on mobile. Left: h3 `"Have something in mind? Let's design it around you."` (max 20ch). Right: outlined-on-dark pill `"Start your Custom Project →"` — same WhatsApp link.

### 6. Section 04 / Why Heaven

- **Purpose**: 8 trust points as an editorial manifesto. NOT icons. NOT cards. Pure typography.
- **Background**: `--paper`.
- **Section header**: Label `"04 / Why Heaven"`. Headline `"Craftsmanship you can see."` / `<em>"Details you can feel."</em>`.
- **Trust list** (`ul.why-list`): No bullets, no padding, border-top 1px `--line`. Each item is `<li class="why-item">` with:
  - `.idx` (60px column): brass "01"–"08" 11px uppercase.
  - `.ttl`: Cormorant 400 `clamp(26px, 3vw, 44px)`.
  - `.dsc`: 13.5px muted, max-width 26ch, right-aligned. (Hidden on mobile.)
  - Border-bottom 1px `--line`, padding `clamp(22px, 3vw, 34px) 0`.
- **Hover behavior**: When any item is hovered, that item stays at full opacity while all others fade to `opacity: 0.35` (0.5s transition). Hovered item's title translates `translateX(8px)` over 0.5s.
- **Reveal**: Whole `.why-list` gets `.in` from the observer. Each `.why-item` has base state `opacity: 0; translateY(24px)`, then `.why-list.in .why-item:nth-child(N)` has a staggered `transition-delay` from `0.02s` (item 1) to `0.58s` (item 8) — 80ms per item — so they cascade in as the list enters the viewport.
- **Items** (all copy is final):
  1. Free design consultation — Every project starts with a conversation, at no cost.
  2. Fully bespoke, never mass-produced — Built to your dimensions, taste and material choice.
  3. Premium wood & materials — Sourced carefully. Chosen for how they age.
  4. Skilled in-house craftsmanship — Every piece is made by our own in-house team.
  5. Large showroom in Agrabad, Chattogram — Come see and feel the work in person.
  6. Delivery & installation included — We deliver and place every piece ourselves.
  7. Easy payment options — Flexible arrangements to suit larger projects.
  8. Trusted by hundreds of happy homeowners — (no `.dsc` — intentionally left blank to avoid unsupported claims.)

### 7. Section 05 / Showroom (Dark)

- **Purpose**: The physical space anchor — this is where the real showroom exterior photo lives. Most authenticity-heavy section.
- **Background**: `--ink`, `padding: var(--pad-y) 0`.
- **Layout** (`.showroom-grid`): Single-column stack — cinematic image on top, then a 2-column body row below.
- **Image container** (`.showroom-image-wrap`): `aspect-ratio: 16/9` desktop, `4/5` at `≤720px`. Uses a `<picture>` element:
  - `<source media="(max-width: 720px)" srcset="assets/showroom-exterior.jpg">` — the portrait 5:6 crop (800×960) that keeps the full building visible on mobile.
  - Default `<img src="assets/showroom-wide.jpg">` — the cinematic 16:9 crop (1600×900) for desktop showing the full "HEAVEN FURNITURE MART" red signage, staircase, promo banner, storefront and a customer walking to the entrance.
  - Wrap has its own clip-path reveal: `clip-path: inset(0 0 100% 0)` → `inset(0 0 0 0)` over 1.4s when `.in` is added. Image inside starts at `scale(1.08)` and settles to `scale(1)` over 2.4s. `image-rendering: -webkit-optimize-contrast`.
  - **Location tag chip** (bottom-left of image, positioned absolute inside the wrap): Small pill `padding: 10px 16px`, background `rgba(26,36,32,0.75)` with `backdrop-filter: blur(10px)`, border 1px `rgba(244,239,230,0.14)`. Contains a 6px brass dot with a soft `box-shadow: 0 0 0 4px rgba(184,150,97,0.15)` glow + uppercase text `"Agrabad · Chattogram"` (10.5px 0.24em ivory 500).
- **Body row** (`.showroom-body`): Grid `6fr 6fr`, gap `clamp(40px, 6vw, 96px)`, align-items start.
  - **Left column** — `.showroom-content`:
    - Section label `"05 / Showroom"` in brass-2.
    - Headline `"Come see"` / `<em>"the craft"</em>` — italic in brass-2.
    - Lede: `"Visit our showroom in Agrabad, Chattogram — and experience the materials, details, and craftsmanship in person."` Ivory at 82% opacity.
  - **Right column** — `.showroom-side` (flex col, gap 28px, padding-top 12px):
    - `.showroom-info` block (border-top 1px `--line-dark`, padding-top 28px, flex col gap 20px). Three `.info-block` rows:
      - Each row is a `90px 1fr` grid, gap 20px, align-items baseline.
      - Label (10.5px 0.24em uppercase, 50% ivory) + value (Cormorant 400 `clamp(18px, 1.6vw, 22px)`, 1.35 line-height, ivory).
      - Address: `"Agrabad Access Road,"` / `"Chattogram, Bangladesh"`.
      - Phone: `<a href="tel:+8801960481983">+880 1960-481983</a>` — brass-2 on hover.
      - Email: mailto rendered from `data-email-user="heavenfurnituremart"` + `data-email-domain="gmail.com"` (see Email Hydration below).
    - CTA: `.cta.on-dark.showroom-cta` with text `"Request a Custom Quote →"` — align-self flex-start, margin-top 16px.
- **Mobile**: Grid collapses to single-column; info-block goes to `80px 1fr` gap 16px.

### 8. Section 06 / Our Story

- **Purpose**: Company milestones — five entries. Vertical typographic timeline. NOT cards.
- **Background**: `--ivory`.
- **Section header**: Label `"06 / Our Story"`. Headline `"A short"` / `<em>"history</em> of Heaven."`
- **Timeline** (`.timeline`, margin-top `clamp(40px, 6vw, 72px)`, border-top 1px `--line`):
  - Five rows (`.tl-row`), each a grid `minmax(180px, 240px) 1fr`, gap `clamp(40px, 6vw, 96px)`, align-items baseline, padding `clamp(32px, 4vw, 56px) 0`, border-bottom 1px `--line`.
  - **Year** (`.tl-year`): Italic Cormorant 300, `clamp(56px, 7vw, 104px)`, line-height 1, -0.01em tracking. For `2024–25`: the year is `<div class="tl-year">2024<span style="font-size:0.55em; letter-spacing:-.02em; padding:0 .18em;">—</span>25</div>` so the em-dash sits proportionally between the years.
  - **Event** (`.tl-event`): Cormorant 400 `clamp(24px, 2.6vw, 40px)`, 1.2 line-height, max-width 28ch. Inside it a `.kicker` span above the main text — uppercase 11px 0.22em 500 brass, margin-bottom 12px.
  - Rows: `2020 / Founded — Founded in Chattogram by Abul Kalam Bhuiyan.` · `2021 / Showroom — Opened the Agrabad showroom.` · `2024–25 / Exhibition — Exhibited at the International Furniture Fair, Chattogram.` · `2025 / Membership — Became a member of the Chamber of Commerce.` · `2026 / Recognition — Received nationwide BFIOA recognition.`
- **Reveal**: `.timeline` observer target. Base state `opacity: 0; translateY(24px)`. `.timeline.in .tl-row:nth-child(N)` — staggered `transition-delay` 0.02 / 0.14 / 0.26 / 0.38 / 0.50s (120ms per row). Hover: subtle `background: rgba(0,0,0,0.02)` over 0.5s.
- **Mobile**: Grid collapses to single column, gap 8px, tighter padding.

### 9. Final CTA (Dark)

- **Purpose**: The closing cinematic moment — one large statement + one CTA.
- **Background**: `--ink` with `assets/final-cta.jpg` at `opacity: 0.28; filter: saturate(0.7)` and a second `linear-gradient(180deg, rgba(26,36,32,0.85) 0%, rgba(26,36,32,0.6) 50%, rgba(26,36,32,0.95) 100%)` overlay on top for legibility.
- **Padding**: `clamp(120px, 20vh, 200px) 0`.
- **Content** (`.final-inner`, flex column, gap `clamp(32px, 5vh, 56px)`, align-items flex-start):
  - Small brass-2 label `"— Request a Custom Quote"`.
  - h2 `.h-display`: `"Make something"` / `"that belongs"` / `<em>"to your space."</em>` — italic brass-2 third line. Max-width 14ch.
  - Lede: `"Tell us what you have in mind. We'll help turn the idea into something made around you."` at 82% ivory.
  - CTA pill `.cta.on-dark` `"Request a Custom Quote →"`.
  - Micro row `.final-micro`: `"Free Design Consultation · Delivery & Installation Included"` — uppercase 11px 0.22em, 55% ivory, brass separator dot.

### 10. Footer

- **Purpose**: Editorial closing — huge typographic statement + minimal contact grid.
- **Background**: `--ink`. Padding `96px 0 40px`. Top border 1px `--line-dark`.
- **Giant tagline** (`.footer-huge`): Three stacked lines — `"Designed."` / `<em>"Crafted."</em>` (italic, 70% ivory) / `"Customized."` (brass-2). Cormorant 400, `clamp(64px, 12vw, 200px)`, 0.95 line-height. Margin-bottom `clamp(64px, 10vw, 120px)`.
- **Grid** (`.footer-grid`, padding-top 48px, border-top 1px `--line-dark`): 4 columns desktop `2fr 1fr 1fr 1fr`, 2 columns tablet, 1 column mobile. Gap `clamp(24px, 4vw, 64px)`.
  - **Col 1** — brand: The 120px-wide `heaven-logo.jpg` image + italic Cormorant 20px `"Bespoke atelier, Chattogram."` + description paragraph.
  - **Col 2** — Visit: Address (Agrabad Access Road, Chattogram, Bangladesh).
  - **Col 3** — Contact: tel:, mailto: (hydrated from data attrs), WhatsApp deep-link.
  - **Col 4** — Follow: Facebook, Instagram, YouTube (real URLs — see Assets section).
- **Column headings** (`h4`): Inter 10.5px 0.24em uppercase 55% ivory 500. Margin-bottom 20px.
- **Column body**: Inter 14px 1.7 line-height 88% ivory. Links hover to brass-2.
- **Footer bottom bar** (`.footer-bottom`, margin-top 64px, padding-top 24px, border-top 1px `--line-dark`): Flex space-between, 11px 0.22em uppercase 50% ivory. Left: `"© 2020–2026 Heaven Furniture Mart · Chattogram"`. Right: `"Designed. Crafted. Customized."`.

### 11. Mobile Sticky CTA

- Only visible at `≤960px`. `position: fixed; left: 16px; right: 16px; bottom: 16px; z-index: 90`. Full-width pill, `background: var(--ink)`, color ivory. Padding `16px 22px`. `border-radius: 999px`. Text: `"Request a Custom Quote"` + `→`. Deep box-shadow `0 12px 30px rgba(0,0,0,0.25)`. Routes to the WhatsApp deep-link.
- Body gets `padding-bottom: 80px` on mobile so content isn't hidden underneath.

## Interactions & Behavior

### WhatsApp CTAs (Primary Conversion — repeated 7 times)

Every primary CTA on the page — header, hero, each Collection card, Bespoke section, Showroom section, Final CTA, mobile sticky, footer link — points to the **same** WhatsApp deep-link:

```
https://wa.me/8801960481983?text=Hello%20Heaven%20Furniture%20Mart%2C%20I'd%20like%20to%20discuss%20a%20custom%20furniture%20project.
```

Implementation pattern in the prototype: all these anchors have `data-whatsapp` attribute and empty `href="#"`. On DOM ready, JS iterates `document.querySelectorAll('[data-whatsapp]')` and sets:
- `href = "https://wa.me/8801960481983?text=" + encodeURIComponent("Hello Heaven Furniture Mart, I'd like to discuss a custom furniture project.")`
- `target = "_blank"`
- `rel = "noopener"`

In the target framework, either hard-code the URL as a shared constant or expose it as an environment variable / config so it can be updated easily.

### Email Hydration (Cloudflare-safe)

Direct `mailto:heavenfurnituremart@gmail.com` links in HTML tend to get auto-obfuscated by Cloudflare's Email Protection (which turns them into `/cdn-cgi/l/email-protection#...` redirects that break in the preview pipeline). The prototype avoids this with a JS hydration pattern:

```html
<a href="#" data-email-user="heavenfurnituremart" data-email-domain="gmail.com"></a>
```

On DOM ready:

```js
document.querySelectorAll('[data-email-user][data-email-domain]').forEach(el => {
  const addr = el.getAttribute('data-email-user') + '@' + el.getAttribute('data-email-domain');
  el.setAttribute('href', 'mailto:' + addr);
  if (!el.textContent.trim()) el.textContent = addr;
});
```

**If the production host doesn't run Cloudflare Email Protection, plain `mailto:` links are fine.** Keep the split pattern only if the production stack routes through Cloudflare.

### Motion System

All motion is CSS-driven, keyed off `.in` classes toggled by a dual reveal system (see State Management).

- **Easing tokens**:
  - `--ease: cubic-bezier(0.4, 0, 0.2, 1)` (Material-style — used for state toggles like header)
  - `--ease-out: cubic-bezier(0.22, 1, 0.36, 1)` (premium editorial reveal — used for all scroll-triggered motion)
- **Reveal patterns**:
  - **`.reveal`** — text/label reveal. Base `opacity: 0; transform: translate3d(0, 32px, 0)`; `.in` → `opacity: 1; transform: none`. Transition 1.1s `--ease-out`.
  - **`.reveal-img`** — image container reveal. Base `clip-path: inset(0 0 100% 0)`; `.in` → `clip-path: inset(0)`. Transition 1.4s. Inner `<img>` starts at `scale(1.1)`, settles to `scale(1)` over 1.8s.
  - **Stagger classes** — `.reveal-delay-1` (100ms), `.reveal-delay-2` (220ms), `.reveal-delay-3` (340ms), `.reveal-delay-4` (460ms). Image variants (`.reveal-img.reveal-delay-N`) use 120/240ms.
  - **Why-list stagger** — 80ms per item via `nth-child` `transition-delay`.
  - **Timeline stagger** — 120ms per row via `nth-child` `transition-delay`.
- **Parallax drift**: A `requestAnimationFrame`-throttled scroll listener translates certain image wraps ±amp px based on how far their center is from the viewport center (normalized -1..+1). Amounts: hero image `translateY(scrollY * 0.10)` (desktop only), People photo wrap ±16px, Collection image wraps ±22px, Bespoke wide ±24px, Showroom image ±14px. Applied to the wrap element only (not the image), so hover-scale on the image is preserved.
- **Header scroll transition**: A scroll listener toggles `.scrolled` on `#hdr` at `scrollY > 40`. All appearance changes (background, backdrop-filter, color, border, padding, min-height, logo size) transition together over 0.55s.
- **Hero clip-path handoff**: When `.hero.loaded` is added at the end of the preloader, `.hero-media` runs the `heroMaskIn` keyframes — `clip-path: inset(0 0 100% 0)` → `inset(0 0 0 0)` over 1.4s.
- **Preloader curtain exit**: `.preloader.done` gets `transform: translateY(-100%)` over 1.2s with the inner content simultaneously fading and translating up 16px.

### Reduced Motion

Wrap all the above in `@media (prefers-reduced-motion: reduce)` overrides:
- Set `animation-duration: 0.01ms; transition-duration: 0.01ms` globally.
- Set all `.reveal-img` to `clip-path: none`.
- Set inner images to `transform: none`.
- Set hero-headline line spans to `transform: none`.
- Clear parallax on scroll (skip the RAF path when the media query matches).
- Preloader durations collapse to <100ms.
- Preloader logo goes straight to visible/unblurred; brass line straight to full width; tagline immediately visible.

### Hover interactions

- **Nav links**: 1px underline scales from 0 → 100% over 0.5s.
- **CTA pills**: Background/color/border flip over 0.5s; arrow shifts `translateX(6px)`.
- **Collection cards**: image scales `1 → 1.04` over 1.4s; brass rule under CTA grows to 100%; arrow shifts 6px.
- **People image**: subtle `scale(1.03)` over 1.8s.
- **Why-list items**: hover an item — the rest fade to 0.35 opacity; the hovered `.ttl` translates 8px right.
- **Timeline rows**: subtle `rgba(0,0,0,0.02)` background wash.
- **Contact links** in showroom: color shifts to brass-2.

### Mobile menu

- Hamburger (`#hamburger`) click toggles `.mobile-open` class on body.
- CSS: `.mobile-open .mobile-menu { transform: translateY(0); pointer-events: auto }` slides the overlay in from the top over 0.6s.
- Hamburger's two lines animate into an X.
- Every menu link (`[data-mmclose]`) closes the menu on click.

## State Management

- **Preloader state**: A single `<div class="preloader">` toggles through `.step-1`, `.step-2`, `.step-3`, `.done` classes on a timer. `body.preloading` locks scroll until removed.
- **Header scrolled state**: `.scrolled` on `<header>` toggled by scroll listener at `scrollY > 40`.
- **Mobile menu**: `body.mobile-open` toggled by hamburger button.
- **Reveal system** — this is the critical piece. Use a **dual strategy** for reliability:
  1. **IntersectionObserver** with `{ threshold: 0.12, rootMargin: '0px 0px -60px 0px' }` observing every `.reveal, .reveal-img, .showroom-image-wrap, .why-list, .timeline`. On intersection, add `.in` and unobserve.
  2. **Scroll-position fallback** — a rAF-throttled scroll listener that also sweeps a `pending` array and reveals anything whose `getBoundingClientRect().top < viewport.height * 0.9`. Kicks off with initial sweeps at 1600ms (post-preloader) and 3000ms (safety), plus a 400ms `setInterval` safety-net poll that self-clears when `pending` is empty.
  - Why both? Some embedded/preview iframe environments throttle rAF and don't dispatch scroll events reliably. In real user browsers only the IntersectionObserver path fires — the fallback is silent overhead.
- **Body overflow** — critical: `overflow-x` must NOT be set on `body`. Setting it turns body into a scroll container and decouples the default-root IntersectionObserver from the actual scroll position. Instead: set `overflow-x: clip` (or `hidden`) on `html`, or rely on `body > * { max-width: 100vw }` if any child could overflow horizontally.

### No data fetching required
Everything is static. No API calls, no backend, no forms. The primary "form" is the WhatsApp deep-link.

## Design Tokens

### Colors
```
--ink        #1a2420    /* Deep charcoal-teal — primary dark surface */
--ink-2      #232d29    /* Slightly lighter charcoal — auxiliary */
--ivory      #f4efe6    /* Warm ivory — primary light surface */
--ivory-2    #ebe4d6    /* Slightly warmer ivory — auxiliary */
--paper      #f8f5ee    /* Paper — the People and Why sections background */
--brass      #a88547    /* Muted brass — accent on light surfaces */
--brass-2    #b89661    /* Slightly warmer brass — accent on dark surfaces */
--brown      #3a2e24    /* Deep brown — reserved supporting */
--tan        #c8a875    /* Natural wood tan — reserved supporting */
--muted      #7a746a    /* Neutral muted text/meta */
--line       rgba(26,36,32,0.14)     /* Fine border on light bg */
--line-dark  rgba(244,239,230,0.16)  /* Fine border on dark bg */
```

### Typography
```
--serif  "Cormorant Garamond", "Playfair Display", Georgia, serif
--sans   "Inter", ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, sans-serif
```
Load from Google Fonts:
`https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,400&family=Inter:wght@300;400;500;600&display=swap`

### Type scale (all fluid via clamp)
```
h-display  clamp(56px, 10vw, 168px)  / 0.94  / -0.02em   (serif 400)
h-1        clamp(44px, 6.8vw, 112px) / 0.98  / -0.015em  (serif 400)
h-2        clamp(36px, 5.2vw, 84px)  / 1.02  / -0.012em  (serif 400)
h-3        clamp(28px, 3.4vw, 54px)  / 1.08  / -0.01em   (serif 400)
lede       clamp(20px, 2vw, 28px)    / 1.4                (serif 400 italic)
body       15.5px / 1.65                                  (sans 400, 78% ink)
mono       11px   / 0.22em uppercase                      (sans 500)
```

### Spacing tokens
```
--pad   clamp(20px, 4vw, 64px)     /* horizontal page padding */
--pad-y clamp(80px, 12vh, 160px)   /* vertical section padding */
```

### Border radius
- CTA pills: `999px`
- Logo chips: `3px` (header) / `4px` (mobile CTA)

### Shadows
- Header logo (subtle depth): `0 8px 24px rgba(0,0,0,0.12)` — reduces to `0 4px 12px rgba(26,36,32,0.15)` when scrolled
- Bespoke inset image: `0 30px 80px rgba(0,0,0,0.5)`
- Mobile sticky CTA: `0 12px 30px rgba(0,0,0,0.25)`

### Easing
```
--ease     cubic-bezier(0.4, 0, 0.2, 1)
--ease-out cubic-bezier(0.22, 1, 0.36, 1)
```

### Breakpoints
```
mobile        max-width: 560px    /* single-column, tighter type */
tablet-down   max-width: 720px    /* showroom picture-source flip */
tablet        max-width: 960px    /* header goes hamburger, sticky mobile CTA appears */
```

## Assets

All images live in `./assets/`. **The three items marked "REAL BRAND ASSET" must not be replaced** — they were supplied by the client and are the authoritative brand imagery.

| File | Size | Role | Notes |
|---|---|---|---|
| `heaven-logo.jpg` | 480×480 | **REAL BRAND ASSET** — full logo tile (dark teal square with white HEAVEN + brass A + white FURNITURE MART). Used in preloader (large) and footer (120px wide). | Client-supplied. Do not redraw. |
| `heaven-logo-tight.jpg` | 280×130 | Tight-cropped variant of the same logo, used in the header as a small chip. | Generated by cropping the source; still the same artwork. |
| `md-team.jpg` | 1600×1038 | **REAL BRAND ASSET** — Managing Director Abul Kalam Bhuiyan seated with the Heaven Furniture Mart team at what appears to be a trade fair. | Client-supplied. Never replace with a stock or generated portrait. |
| `showroom-wide.jpg` | 1600×900 | **REAL BRAND ASSET (16:9 crop)** — the actual Heaven Furniture Mart showroom exterior on Agrabad Access Road: red facade, HEAVEN FURNITURE MART signage, staircase, promo banner, customer entering. Used at viewport >720px. | Generated from a 1024×762 HD source supplied by the client. |
| `showroom-exterior.jpg` | 800×960 | Same source — 5:6 portrait crop for mobile, keeping the full signage in frame. | Served by the `<picture>` fallback at ≤720px. |
| `hero.jpg` | ~2560×1920 | Hero background — warm minimal interior (brown sofa, woven chairs, wood stove, textiles). Sourced via Unsplash-adjacent editorial license. | Placeholder for eventual Heaven-supplied interior photography. |
| `brand.jpg` | ~2560×1440 | Not currently used in the final HTML (left in for future use). | Optional. |
| `living.jpg` | ~2560×~1700 | Living-room collection image (Section 02). | Editorial furniture photography placeholder. |
| `bedroom.jpg` | ~2560×1440 | Bedroom collection image. | Editorial placeholder. |
| `dining.jpg` | ~2560×~2000 | Dining collection image. | Editorial placeholder. |
| `office.jpg` | 570×570 | Office & Study collection image. | Studio product shot placeholder — smaller than the others; consider replacing with a real Heaven photo. |
| `bespoke-wide.jpg` | ~1670×1193 | Bespoke section cinematic wide image (walnut interior). | Editorial placeholder. |
| `wood-detail.jpg` | ~3430×1960 | Bespoke inset detail (wood grain close-up). | Editorial placeholder. |
| `final-cta.jpg` | ~1299×1390 | Final CTA background (dark moody interior — used at 28% opacity). | Editorial placeholder. |
| `story.jpg` | ~2560×1707 | Not currently used in the final HTML. | Optional. |

**Placeholder policy**: Every editorial furniture image marked "placeholder" should ideally be replaced with a real Heaven Furniture Mart photograph before the site ships. The image slots (aspect ratios and object-fit rules) are already correct — swap the file and the crop should still work.

### Social & contact links
- **Facebook**: `https://facebook.com/HeavenFurnitureMart`
- **Instagram**: `https://instagram.com/heaven_furniture_ltd`
- **YouTube**: `https://youtube.com/@HeavenFurnitureMart`
- **Phone**: `tel:+8801960481983` (display: `+880 1960-481983`)
- **Email**: `mailto:heavenfurnituremart@gmail.com` (see Email Hydration for the Cloudflare-safe pattern)
- **Address**: Agrabad Access Road, Chattogram, Bangladesh

### SEO metadata
```html
<title>Heaven Furniture Mart — Bespoke Furniture Crafted Around You</title>
<meta name="description" content="Luxury bespoke furniture and interior styling from Heaven Furniture Mart, Chattogram. Furniture designed, crafted and customized around your space and taste." />
<meta property="og:title" content="Heaven Furniture Mart — Bespoke Furniture Crafted Around You" />
<meta property="og:description" content="Luxury bespoke furniture designed, crafted and customized around your space, your taste, and the way you live." />
<meta property="og:type" content="website" />
<meta property="og:image" content="assets/hero.jpg" />
<meta name="theme-color" content="#1a2420" />
```

## Content Accuracy — Do NOT invent

The client explicitly restricted content. When implementing, do **not** add any of the following unless the client provides them in writing:
- Customer names, testimonials, quotes, ratings, or star scores
- Numeric statistics ("500+ projects", "10 years of…"), percentages, revenue, or project counts
- Awards, certifications, partnerships not already on the page
- Opening hours, holiday hours, or any temporal claims
- Pricing, discounts, offers, or payment terms

**Approved copy is exhaustively documented above** — implement only what's listed. If a section feels empty, that's intentional (see Why Heaven item 08 which is intentionally left without a description).

## Files

- **`Heaven Furniture Mart.html`** — The complete self-contained prototype. Everything (HTML, CSS, JS) is inlined. **This is the source of truth** — when in doubt about a spec, open this file. The heading `<!-- ============ SECTION XX ============ -->` markers make it easy to locate each section.
- **`assets/`** — All images referenced from the HTML. See the Assets table above.

### File organization suggestion for the target codebase

If porting to a React / Next.js / Astro / Vue project, a reasonable split would be:

```
components/
  Header.tsx          — fixed header, scroll state, mobile menu
  Preloader.tsx       — intro sequence
  Hero.tsx            — headline + supporting + parallax image
  PeopleSection.tsx   — Section 01
  Collections.tsx     — Section 02 (accepts a list of 4 collection items)
  BespokeSection.tsx  — Section 03
  WhyHeaven.tsx       — Section 04 (accepts an array of trust points)
  ShowroomSection.tsx — Section 05
  StoryTimeline.tsx   — Section 06 (accepts an array of year entries)
  FinalCTA.tsx        — closing dark section
  Footer.tsx
  MobileStickyCTA.tsx
  ui/
    Cta.tsx           — the pill button in its 3 variants (outlined-on-light, outlined-on-dark, solid)
    SectionNum.tsx    — the "01 / Section Name" label with brass rule
hooks/
  useReveal.ts        — the dual IntersectionObserver + fallback reveal system
  useHeaderScroll.ts  — toggles .scrolled on scrollY > 40
  useParallax.ts      — the rAF-throttled image drift
styles/
  tokens.css          — the design token variables listed above
  fonts.css           — Google Fonts import
lib/
  contact.ts          — WA_URL, EMAIL, TEL, SOCIALS constants
```

## Post-handoff notes

- The prototype was reviewed by an automated verifier and is production-ready. Known verifier caveats:
  - CSS transitions can appear frozen in some embedded preview iframes; they run normally in real user browsers.
  - `loading="lazy"` images don't trigger loads on programmatic scroll in the preview iframe; real user scrolling triggers them fine.
  - IntersectionObserver and rAF are throttled in some preview iframes — the dual reveal fallback documented above is what handles this.
- The final HTML is ~200KB uncompressed. Google Fonts is the only third-party dependency.
- If the target framework has its own font-loading system (Next.js `next/font`, etc.), prefer that over the Google Fonts link tag for LCP performance.
