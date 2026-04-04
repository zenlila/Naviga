# Sophi — Figma-to-Code Project Tracker

## Project Overview
**Figma File**: `1NoXKFA7SpaAwyPR0dvePY` (Sophi)
**Authenticated as**: Çağatay Kemal Tok (cagataytok@gmail.com)
**Date Started**: 2026-03-28

---

## Design System Tokens
- **Font**: Google Sans (Medium, Bold, Regular), Poppins (Regular — captions)
- **Primary Purple Gradient**: `linear-gradient(~115-138deg, #2E0081 → #5048D1)`
- **Dark Purple**: `#2E0182`, `#1F0059`
- **Text Colors**: Black `#000`, Gray `#5A5A5A`, Light Gray `#9D9D9D`, Caption `#6C6C6C`, Stat Label `#AEAEAE`
- **Link Color**: `#2E0182` (underlined), `#8E2CFF` (variant)
- **Background**: White `#FFF`, Light Gray `#F3F3F3`, Frosted glass `rgba(237,237,237,0.4)`
- **Border Radius**: 20px (small), 30px (stats/buttons), 40px (cards/nav), 50px (tags), 60px (testimonials), 80px (large sections/CTA)
- **Shadows**: `0px 10px 30px rgba(0,0,0,0.1)` (cards), `inset 0px 0px 80px rgba(174,0,255,0.8)` (CTA glow), `inset 0px 0px 100px rgba(136,0,255,0.8)` (section glow)
- **Desktop Width**: ~1280px (max-content ~1040-1080px)
- **Mobile Width**: ~430px

---

## Page Inventory

### Layout Convention
Desktop frames are placed on the left; Mobile frames are directly to the right of their desktop counterpart.

| # | Page | Desktop Node ID | Mobile Node ID | Desktop Fetched | Mobile Fetched | Implementation Status |
|---|------|----------------|----------------|-----------------|----------------|----------------------|
| 1 | **Mainpage** | `46:2165` | `47:2590` | ✅ Code + Screenshot | ✅ Code + Screenshot | ❌ Not started |
| 2 | **Journal** | `50:2528` | `160:799` | ✅ Code + Screenshot | ✅ Fixed in Figma | ✅ Mobile Figma fixed |
| 3 | **Article** | `50:2975` | ❌ Not designed yet | ✅ Screenshot | — | ❌ Not started |
| 4 | **About** | `50:3215` | ❌ Not designed yet | ✅ Screenshot | — | ❌ Not started |
| 5 | **Contact** | `50:3351` | ❌ Not designed yet | ✅ Screenshot | — | ❌ Not started |
| 6 | **Book a Demo** | `93:1640` | ❌ Not designed yet | ✅ Screenshot | — | ❌ Not started |

---

## Page Summaries

### 1. Mainpage (Desktop: `46:2165` / Mobile: `47:2590`)
- **Sections**: Navigation → Hero (AI-Driven Commerce + interactive product card demo) → "Your search bar is losing you revenue" (3 value cards) → "Meet Sophi — That reads intent" (conversational search demo + feature list) → "Conversational commerce" (dark purple section, 3 cards + Architecture) → "Real results, Real revenue" (6 stat cards in 3x2 grid) → Case Study (Visa) → Blog (3 article cards) → Testimonial slider → CTA (Request a Demo) → Footer
- **Mobile adaptations**: Stacked single-column layout, smaller typography (110px→50px headings, 48px→24-28px subheadings), stats in 2-column grid, testimonial becomes single card, horizontal tag bar becomes dropdown, hero simplified

### 2. Journal (Desktop: `50:2528` / Mobile: `160:799`)
- **Sections**: Navigation → Header ("Latest updates from Agent commerce") → Featured article (full-width) → Article grid (2 columns, 4 cards) → Subscribe CTA ("Subscribe to Sophi journal") → Footer
- **Mobile adaptations**: Single column, smaller cards with thumbnails beside text

### 3. Article (Desktop: `50:2975`)
- **Sections**: Navigation → Article header (category, title, hero image with author/date overlay) → Body text (rich markdown-like content with subheadings) → Recent articles (3 thumbnails) → Footer
- **No mobile version in Figma** — needs to be derived from desktop

### 4. About (Desktop: `50:3215`)
- **Sections**: Navigation → Hero banner ("Intents are fascinating us continuously") → Company description + stats (1,400+ brands, 33 patents, 250M searches) → Mission statement → "Our milestones" timeline (horizontal scrollable) → Footer
- **No mobile version in Figma** — needs to be derived from desktop

### 5. Contact (Desktop: `50:3351`)
- **Sections**: Navigation → Hero ("We'd love to hear from you!") → Trust bar (Visa, Beymen, İş Bankası) → Department options (Sales / HR / General inquiry — 3 cards) → Contact form (name, email, website, use case, source, submit button) → Footer
- **No mobile version in Figma** — needs to be derived from desktop

### 6. Book a Demo (Desktop: `93:1640`)
- **Sections**: Navigation → Hero ("We know your time is valuable, so let's cut to that chase.") → 30-min chat expectations (bullet list) → Testimonial slider (with photos) → Schedule form (name, email, website, use case, source, "Schedule a 30-Minute Meeting" button) → Footer
- **No mobile version in Figma** — needs to be derived from desktop

---

## Shared Components
- **Navigation (Desktop)**: Frosted glass bar, 1100px wide, logo + 4 links + "Book a Demo" button
- **Navigation (Mobile)**: Frosted glass bar, 400px wide, logo + hamburger menu icon (purple gradient)
- **Footer**: Links (Product, Company, Help, Contact) + copyright "© 2026 · All rights reserved"
- **CTA Section**: Deep purple bg with particle mesh image, white heading, white "Request a Demo" button
- **Article Card**: Thumbnail + title + category/read-time metadata

---

## Implementation Plan

### Approach: Multi-page HTML site (or SPA with routing)
Since the current project is a single `index.html` file, we need to decide:
- Option A: Separate HTML files per page (simplest)
- Option B: Single-page with JS-based routing/sections

### Mobile Strategy
For pages **without** Figma mobile designs (Article, About, Contact, Book a Demo):
- Apply the same responsive patterns established in Mainpage & Journal mobile:
  - Headings scale down (~50% of desktop size)
  - 3-column grids → single column stacked
  - Horizontal layouts → vertical stacked
  - Desktop nav → mobile nav with hamburger
  - Section padding/margins reduce proportionally
  - Border radius slightly reduced on outer containers
  - Tags/tabs → dropdown selectors

---

## Desktop → Mobile Responsive Standards (derived from Mainpage)

### Typography Scaling
| Element | Desktop | Mobile | Ratio |
|---------|---------|--------|-------|
| Section subtitle | `48px` | `24-28px` | ~÷2 |
| Section heading (gradient) | `110px`, tracking `-2.2px` | `50px`, tracking `-1px` | ~÷2.2 |
| Body / description | `22-26px` | `18px` | ~÷1.3-1.4 |
| Card title | `42px` | `24px` | ~÷1.75 |
| Card body | `26px` | `18px` | ~÷1.4 |
| Links | `20px` | `18px` | ~÷1.1 |
| Category/meta | `24px` | `14px` | ~÷1.7 |
| Blog card title | `36px` | `18px` | ÷2 |

### Layout Rules
- All side-by-side layouts → vertical stack (`flex-row` → `flex-col`)
- 3-column grids → single column stacked
- Stats grid: 3×2 → 2×3 (CSS grid `grid-cols-2`)
- Tag bars: horizontal multi-label → dropdown with single label + chevron
- Testimonial: horizontal slider → single card, photos removed

### Spacing & Sizing
| Element | Desktop | Mobile |
|---------|---------|--------|
| Section vertical padding | `120-160px` | `60-100px` |
| Section horizontal padding | `20px` (content in max-width container) | `px-[20px]` |
| Content gap (header→content) | `30-60px` | `20-40px` |
| Header text gap (subtitle→heading) | `10-20px` | `10px` |
| Card padding | `p-[40px]` | `p-[40px]` or `px-[30px] py-[20px]` |
| Card internal gap (icon→content) | `40px` | `20px` |

### Border Radius
| Element | Desktop | Mobile |
|---------|---------|--------|
| Large sections | `80px` | `60px` |
| Cards | `40px` | `40px` or `30px` (stats) |
| CTA | `80px` | `80px` (same) |
| Nav | `40px` | `40px` (same) |

### Component Changes
| Component | Desktop | Mobile |
|-----------|---------|--------|
| Navigation | 1100px, logo + 4 links + button | 400px, logo + hamburger icon |
| CTA width | `1260px` | `410px` |
| CTA heading | `50px` | `24px` |
| CTA padding | `px-[160px] py-[140px]` | `px-[40px] py-[130px]` |
| CTA button | `300px` fixed | `100%` full-width |
| Footer | Present | Omitted |

### Content Reduction
- Complex interactive elements simplified or removed (e.g., chat bubbles, analyzing steps)
- Article count may reduce (3→2 in blog section)
- Architecture sub-section removed in mobile
- Testimonial slider → single card

---

## Tooling Capabilities (MCP)

### What We Can Do
| Action | Tool | Status |
|--------|------|--------|
| Read designs from Figma | `get_design_context`, `get_screenshot`, `get_metadata` | ✅ Verified |
| Write/modify designs IN Figma | `use_figma` (Figma Plugin API — JS execution) | ✅ Verified |
| Create new Figma files | `create_new_file` | ✅ Available |
| Capture web pages to Figma | `generate_figma_design` | ✅ Available |
| Implement as HTML/CSS code | Manual conversion from `get_design_context` output | ✅ Verified |

### Workflow for Creating Mobile Frames
1. Load `figma-use` skill (MANDATORY before every `use_figma` call)
2. Use `use_figma` with Plugin API JS to create/modify frames
3. Can clone nodes, set auto-layout, text styles, fills, effects, images
4. Verify result with `get_screenshot`

---

## Journal Mobile — Fix Plan

### Completed Fixes (2026-03-28)
All changes made via `use_figma` Plugin API:

| Fix | Node IDs | Status |
|-----|----------|--------|
| Header text: "Latest updates from" | `160:806` | ✅ Done |
| Header heading: "Agent commerce" (50px gradient) | `160:807` | ✅ Done |
| Featured article card (vertical: image→meta→title→desc→link) | `185:799` (cloned from mobile card `160:940`) | ✅ Done |
| Featured card image (full-width, 200px, rounded top) | `185:800` | ✅ Done |
| Featured card title (24px, bold, black) | `185:802` | ✅ Done |
| Featured card description (18px, #737373) | `188:799` | ✅ Done |
| Featured card link "Explore the platform" (18px, #2F0183, underline) | `188:800` | ✅ Done |
| Removed redundant blog header "Latest updates from agent commerce." | `160:937` | ✅ Removed |
| CTA text: "Subscribe to Sophi journal." | `160:972` | ✅ Done |
| CTA button: "Sign up to newsletter" | `160:975` | ✅ Done |
| 2 compact article cards kept | `160:940`, `160:948` | ✅ Unchanged |
| "View all articles" link kept | `160:956` | ✅ Unchanged |
| Footer omitted | — | ✅ Per mobile standard |

### Known Limitation
- Figma screenshot API may show cached/stale content. All changes confirmed via API read-back.
- Google Sans font cannot be loaded via Plugin API (`loadFontAsync` fails). Workaround: clone existing nodes that already use the font, then modify `.characters` directly (works without font loading on pre-existing font assignments).

---

## Notes & Context
- Figma asset URLs expire after 7 days — re-fetch before implementation if needed
- The project currently uses vanilla HTML/CSS/JS (no framework, no Tailwind)
- All Figma code output is React+Tailwind reference only — must be converted to vanilla HTML/CSS
- Desktop-first approach: implement desktop, then add responsive breakpoints for mobile
