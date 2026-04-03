# KEYSTONESYSTEMS — Marketing Site
## Claude Code Build Instructions

---

## Project Overview

This is the static marketing website for **KEYSTONESYSTEMS**, a claims technology company headquartered in Waco, TX. The site lives at **keystonestack.com** and serves as the parent brand hub that introduces the product suite and directs visitors to the two flagship products: **INSPEKTiT** and **INSPEKTiQ**.

No backend. No framework. Plain HTML, CSS, and JavaScript only. Supabase auth integration will be added in a future phase — placeholders only for now.

---

## Repo & Deployment

- **GitHub:** `keystonesystem1/KEYSTONESYSTEMS`
- **Deployed via:** Vercel (auto-deploys on push to `main`)
- **Live URL:** keystonestack.com / www.keystonestack.com
- **Vercel project:** keystonesystems (under keystonesystem1 org)

---

## File Structure

```
/
├── index.html              ← Homepage (primary marketing page)
├── splash.html             ← Post-login loading/welcome screen
├── account.html            ← User account dashboard
├── /assets
│   ├── /css
│   │   └── shared.css      ← Shared variables, resets, typography
│   ├── /js
│   │   └── shared.js       ← Shared utility functions
│   └── /img                ← Logos, icons, any static images
├── /reference              ← Mike Weaver's source files (DO NOT MODIFY)
│   ├── Keystone_Homepage_v44_LOCKED.html
│   ├── Keystone_Account_Page_v1.html
│   ├── Keystone_Adjuster_Portal_v2.html
│   ├── Keystone_Splash_v1.html
│   └── Keystone_BrandReference_v1.pdf
└── CLAUDE.md               ← This file
```

---

## Source of Truth

**Mike Weaver's files in `/reference` are the design and content source of truth.** Do not deviate from his layout, copy, color usage, or component patterns unless:
- There is a technical bug that must be fixed, OR
- A deviation is explicitly documented in a build brief

The brand reference PDF (`Keystone_BrandReference_v1.pdf`) is the locked brand standard. Follow it exactly.

---

## Brand Standards (from Keystone_BrandReference_v1.pdf)

### Company Name
- Always written: `KEYSTONESYSTEMS` (one word, all caps, no space)
- "KEYSTONE" in white `#F2F2F4`, "SYSTEMS" in bronze `#C9A84C`
- Font: Orbitron 900 — wordmarks only

### Product Wordmarks
| Product | Treatment |
|---|---|
| INSPEKTiT | INSPEKT white, `iT` white inside L-bracket, bracket color `#4298CC` |
| INSPEKTiQ | INSPEKT white, `iQ` in sage green `#5BC273` — no bracket |
| INSPEKTiV | INSPEKT white, `iV` in rose `#E05C8A` — no bracket — COMING SOON only |

All wordmarks: Orbitron 900, locked.

### Color System
| Name | Hex | Usage |
|---|---|---|
| Bronze | `#C9A84C` | KEYSTONESYSTEMS SYSTEMS suffix, CTAs, accents |
| Brand Blue | `#4298CC` | INSPEKTiT bracket and accent |
| Sage Green | `#5BC273` | INSPEKTiQ accent |
| Rose | `#E05C8A` | INSPEKTiV accent (coming soon only) |
| Background | `#0A0A0A` | All page backgrounds |
| White | `#F2F2F4` | Primary text |
| Muted | `#64646C` | Secondary text |

### Typography
- **Orbitron 900** — product wordmarks ONLY. Never for body, headings, or labels.
- **Barlow Condensed** (600/700/800/900) — all headings, nav, CTAs, labels, pills, badges
- **Barlow** (300/400/500) — all body copy and prose
- Never use Inter, Roboto, Arial, or system fonts

### Rules
- Never add a space between KEYSTONE and SYSTEMS
- Never apply the L-bracket to INSPEKTiQ or INSPEKTiV
- Never use orange on any Inspekt suite product
- Never mention ClaimGen — it is on hold pending attorney review

---

## Pages

### 1. index.html — Homepage

Base file: `Keystone_Homepage_v44_LOCKED.html`

**Implement as-is with these specific changes:**

- Fix CSS bug: `.hero-suite` class is missing its selector name (line ~258 in source — `display: flex; gap: 3px;` block has no class name before it)
- INSPEKTiV appears in the product stack and audience tabs — replace all INSPEKTiV full cards with a **"Coming Soon"** placeholder card. Keep the visual slot, dim it to ~50% opacity, show the wordmark and a "Coming Soon" pill. No flip interaction.
- Footer: remove INSPEKTiV as a nav link, replace with `INSPEKTiV — Coming Soon` at reduced opacity, no href
- Auth modal (Login / Create Account): replace the sign-in form and create account form with an **early access capture** UI:
  - Heading: "Full login is coming soon."
  - Subtext: "We're currently onboarding early access users. Enter your email and we'll notify you the moment accounts open."
  - Single email input field
  - CTA button: "Notify Me When It's Live →" (sign in tab) / "Get Early Access →" (create account tab)
  - Role selector (Adjuster / IA Firm / Carrier) on the create tab — kept for context, no backend action
  - On button click: show inline confirmation message "You're on the list. We'll be in touch." — no actual form submission yet
  - Note below button: "No spam. One email when accounts open."
- All other content, sections, copy, and interactions: implement exactly as Mike built them

### 2. splash.html — Welcome Screen

Base file: `Keystone_Splash_v1.html`

Implement exactly as-is. The only change: after the progress bar completes, redirect to `account.html` instead of `/adjuster`. Update the portals object:
```js
var portals = {
  adjuster: 'account.html',
  firm:     'account.html',
  carrier:  'account.html',
};
```

### 3. account.html — User Dashboard

Base file: `Keystone_Account_Page_v1.html`

**Implement with these changes:**

- Replace INSPEKTiV (active product) with **INSPEKTiT** as the primary enrolled product card
- Replace INSPEKTiT (not enrolled) with **INSPEKTiQ** as the second product card
- Add a third card for **INSPEKTiV** styled as "Coming Soon" — dimmed, no Open/Add button, just a "Coming Soon" pill
- "Open INSPEKTiT →" button: links to `https://inspektit-app.vercel.app` for now (placeholder until inspektit.io is live)
- "Open INSPEKTiQ →" button: links to `https://inspektiq.io` for now
- "Add" buttons: show an inline message "Coming soon — contact your account manager to add this product." No backend action yet.
- Nav logo links back to `index.html`
- The adjuster portal page (`Keystone_Adjuster_Portal_v2.html`) is a future phase — do not build it yet

---

## Navigation Flow

```
keystonestack.com (index.html)
    ↓ user clicks Login/Create Account
    → modal opens (early access capture — no real auth yet)
    
    ↓ [future: real auth → splash.html → account.html]
    
account.html
    ↓ "Open INSPEKTiT →"
    → inspektit-app.vercel.app (existing app)
    
    ↓ "Open INSPEKTiQ →"  
    → inspektiq.io (existing app)
```

---

## Shared Assets

Extract these from Mike's files into `/assets/css/shared.css`:
- CSS custom properties (`:root` variables) — single source of truth for all colors, surfaces, borders
- Font imports (Google Fonts — Orbitron, Barlow Condensed, Barlow)
- Base reset (`*, *::before, *::after`)
- Body base styles

Each page should `<link>` to `shared.css` rather than duplicating these declarations.

---

## What NOT to Build (Yet)

- No real authentication or Supabase integration
- No backend, API calls, or form submissions
- No adjuster portal page
- No INSPEKTiV full product page
- No ClaimGen mentions anywhere
- No NspectPro mentions on any Inspekt suite page

---

## Coding Standards

- Semantic HTML5
- CSS custom properties for all colors and spacing — no hardcoded hex values outside of `:root`
- Vanilla JS only — no frameworks, no npm, no build step
- All pages must be fully self-contained and work by opening the HTML file directly (no dev server required)
- Mobile responsive — follow breakpoints already established in Mike's files (`max-width: 960px`)
- No external dependencies beyond Google Fonts and the fonts already used

---

## Branch Strategy

- `main` — production, auto-deploys to keystonestack.com
- Feature work should be done on a branch and merged via PR

---

## Questions / Decisions Log

| Date | Decision |
|---|---|
| 2026-04-03 | Plain HTML/CSS/JS confirmed — no framework |
| 2026-04-03 | INSPEKTiV shown as Coming Soon only — not a full product card |
| 2026-04-03 | Auth modal replaced with early access email capture for launch |
| 2026-04-03 | Supabase auth integration deferred to future phase |
| 2026-04-03 | Password protection on Vercel deferred — too costly for testing phase |
