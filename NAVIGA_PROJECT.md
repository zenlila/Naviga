# Naviga Yachting — Interactive Yacht Selector

**Project:** Web-based yacht browsing experience for navigayachting.com
**Target:** WordPress template replacement (MVP as standalone HTML/CSS/JS first)
**Started:** 2026-03-13

---

## Design Source

**Figma file:** `gV8nf3V8KeJTDS6uLfYBPQ` — Frame: "Mainpage - Ready to Code" (`25:217`)
**Design resolution:** 1920x1080

### Figma Assets Collected
| Asset | Node ID | Type |
|-------|---------|------|
| Logo: naviga-yachting | `25:300` | SVG/Image |
| flag-icon: Turkey | `25:299` | 16x16 image |
| flag-icon: Croatia | `25:297` | 16x16 image |
| flag-icon: Greece | `25:298` | 16x16 image |
| Aesthetic Title Items (decorative chevron + lines) | `28:448` | SVG/Image |
| Full page screenshot | `25:217` | Reference |

> **Note:** Figma MCP asset URLs expire after 7 days. Download or re-fetch before building.

---

## Architecture

### Layout (from Figma)
```
┌─────────────────────────────────────────────────────┐
│  Background: gradient #e3efef → #d2fffc             │
│  + Three.js dot-wave canvas (Phase 2)               │
│  + Country dot-map bottom-right (Phase 2)           │
│                                                      │
│  ┌──────┐                                            │
│  │ LOGO │     ┌─ MAIN CARD (920px) ──────────────┐  │
│  └──────┘     │ ┌─ Frosted Header ─────────────┐ │  │
│               │ │  Country Tabs: All|GR|TR|HR   │ │  │
│  ┌─────────┐  │ │  Month Slider (iOS-style)     │ │  │
│  │ Side    │  │ └───────────────────────────────┘ │  │
│  │ Carousel│  │                                    │  │
│  │ Left    │  │  ┌─ Yacht Image ───────────────┐  │  │
│  │         │  │  │                              │  │  │
│  └─────────┘  │  │   (3D perspective carousel)  │  │  │
│               │  │                              │  │  │
│               │  │  ┌─ Frost Blur ───────────┐  │  │  │
│               │  │  │  ⌄ decorative lines    │  │  │  │
│  ┌─────────┐  │  │  │  YACHT NAME           │  │  │  │
│  │ Side    │  │  └──┴────────────────────────┘  │  │  │
│  │ Carousel│  │                                    │  │
│  │ Right   │  │  ┌─ Dashboard ─────────────────┐  │  │
│  │         │  │  │ Specs | 5  10  4 | Amenities│  │  │
│  └─────────┘  │  └─────────────────────────────┘  │  │
│               │                                    │  │
│               │  ┌─ CTA ───────────────────────┐  │  │
│               │  │ [Watch] VIDEO CALL [Schedule]│  │  │
│               │  └─────────────────────────────┘  │  │
│               └────────────────────────────────────┘  │
│                                                      │
│                              Country Map + "TURKEY"  │
└─────────────────────────────────────────────────────┘
```

### Key Components
1. **Country Tabs** — Pill buttons (All / Greece / Turkey / Croatia) with flag icons. "All" has white fill, others have white border on frosted glass.
2. **Month Slider** — iOS-style horizontal picker from `ios-horizontal-picker-demo.html`. Infinite scroll, drag/snap, occupancy % bars with color coding.
3. **Yacht Carousel** — 3D perspective carousel. Active yacht fills main card image area. Side yachts peek behind card with depth + rotation. Drag/swipe + click navigation.
4. **Yacht Dashboard** — Left: spec labels + values. Center: big numbers (Cabins, Guests, Crew). Right: amenities list.
5. **CTA Buttons** — Teal primary "Video Call Now" with glow. Two overlay sub-buttons "Watch Now" / "Schedule".
6. **Background** — Phase 1: CSS gradient. Phase 2: Three.js dot-wave + country dot-map.

### Data
- Yacht database from `naviga-yacht-selector.html` (real navigayachting.com fleet)
- 3 countries: Greece (5 yachts), Turkey (8 yachts), Croatia (5 yachts)
- Occupancy data per country per month
- Yachts filtered by selected country + month availability

### Fonts
- **Inter** — UI text (weights: 200, 300, 400, 500, 600, 700)
- **Cormorant Garamond** — Yacht name display (weight: 400)

---

## Phases

### Phase 1 — MVP (Current)
**Goal:** Pixel-accurate implementation of Figma design with all interactive components working.

**Scope:**
- [x] Collect all Figma assets (logo, flags, decorative elements)
- [x] Collect design specs (colors, sizes, layout, fonts)
- [x] Build HTML structure matching Figma layout
- [x] CSS: gradient background, main card, frosted header, dashboard, CTA
- [x] Country tabs with flag icons (interactive, filters data)
- [x] Month slider (ported from ios-horizontal-picker-demo.html, restyled for frosted glass)
- [x] Yacht carousel (side images + swipe + click navigation + arrow keys)
- [x] Dashboard auto-updates on yacht change
- [x] Yacht filtering by country + month
- [x] Hover/click states on CTA buttons (no real links)
- [x] Placeholder `<canvas>` for Three.js background
- [x] Desktop-first, basic mobile breakpoints
- [x] Visual polish pass — frosted header restructured, distance-based opacity, progressive blur, dashboard centering, font audit, carousel crossfade
- [ ] Final Figma pixel comparison + touch-ups

**File structure:** Single HTML file (inline CSS + JS) in `SpecialProjects/NavigaYachting/`. All assets served locally from `assets/` subfolder.

**NOT in Phase 1:**
- Three.js background
- Country dot-maps
- Real CTA functionality
- Full mobile optimization
- WordPress integration

### Phase 2 — Three.js Background
**Goal:** Animated dot-wave background with country-specific dot-maps.

**Scope:**
- [ ] Three.js dot-wave effect covering full background
- [ ] Country dot-map data (Turkey, Greece, Croatia outlines as dot arrays)
- [ ] Selected country tab → highlights that country's dot-map in bottom-right
- [ ] Smooth transition between country maps
- [ ] Performance: keep it lightweight, requestAnimationFrame-based

### Phase 3 — Polish & Mobile
**Goal:** Full responsive design + interaction polish.

**Scope:**
- [ ] Mobile layout (stacked, touch-optimized)
- [ ] Tablet breakpoint
- [ ] Animation refinements (card transitions, tab switches)
- [ ] Loading states for yacht images
- [ ] Keyboard navigation (arrow keys for carousel)
- [ ] Accessibility basics (ARIA labels, focus states)

### Phase 4 — WordPress Integration
**Goal:** Convert to WordPress template.

**Scope:**
- [ ] Split into separate CSS/JS files
- [ ] WordPress template structure
- [ ] Dynamic yacht data (from WP custom post types or API)
- [ ] CTA buttons wired to real actions (video call booking, etc.)
- [ ] SEO meta tags
- [ ] Performance optimization (lazy loading, image srcset)

---

## Design Tokens (from Figma)

### Colors
| Token | Value | Usage |
|-------|-------|-------|
| bg-gradient-start | `#e3efef` | Page background top |
| bg-gradient-end | `#d2fffc` | Page background bottom |
| card-bg | `#ffffff` | Main card |
| frosted-header-bg | `rgba(162,162,162,0.3)` | Header overlay |
| cta-primary | `#00cec1` | Main CTA button |
| cta-glow | `rgba(23,235,226,0.7)` | CTA shadow |
| cta-sub-bg | `rgba(255,255,255,0.2)` | Sub-button overlay |
| tab-border | `#ffffff` | Country tab border |
| tab-active-bg | `#ffffff` | Active tab fill |
| tab-active-text | `#000000` | Active tab text |
| tab-inactive-text | `#ffffff` | Inactive tab text |
| text-primary | `#000000` | Dashboard text |
| text-muted | `rgba(0,0,0,0.4)` | Spec labels |
| occupancy-red | `#ff0000` / `#ff3946` | High occupancy bars |
| occupancy-orange | `#ff7e39` / `#ff7b39` | Medium-high occupancy |
| occupancy-yellow | `#ffdb39` / `#ffca39` | Medium occupancy |
| occupancy-green | `#c7ff39` | Low occupancy |

### Sizes (from Figma, 1920x1080 canvas)
| Element | Size |
|---------|------|
| Main card | 920 x 966px |
| Card border-radius | 40px top, 20px bottom |
| Frosted header height | 180px |
| Yacht image height | 637px (within card) |
| Country tab | 200 x 36px, radius 20px |
| Month picker selected | 110 x 80px, radius 16px |
| Month picker item | 80 x 60px spacing |
| CTA main button | 912 x 108px, radius 18px |
| CTA sub button | 210 x 70px, radius 10px |
| Dashboard stats font | 48px medium |
| Yacht name font | 54px Cormorant Garamond |
| Side carousel images | ~690x424 (overlap behind card) |

---

## Decisions Log

| Date | Decision | Reason |
|------|----------|--------|
| 2026-03-13 | Single HTML file for Phase 1 | Fastest iteration, easy to preview |
| 2026-03-13 | Keep yacht DB from old file | Real fleet data, already structured |
| 2026-03-13 | 3D perspective carousel (not flat scroll) | Better visual impact, matches Figma depth |
| 2026-03-13 | Three.js deferred to Phase 2 | Focus on core layout + interactions first |
| 2026-03-13 | Desktop-first, mobile planned for Phase 3 | MVP priority is getting the design right |

---

## Changelog

### 2026-03-13 — Session 2: Design Polish Pass

**Applied user's 8-point feedback:**

1. **Frosted header restructured** — Tabs area is now a flex container with `padding: 30px 30px 20px`. Frosted glass bg covers only the tabs, not the slider.
2. **Month slider expanded to full card width** — Picker moved outside frosted header, positioned below it at `top: 86px`. No frosted bg on slider. Implemented iOS-style distance-to-center opacity: ±1=1.0, ±2=0.70, ±3=0.30, ±4=0.10.
3. **Yacht name area** — Decorative asset sized to 722×83px (Figma exact). Name is Cormorant Garamond Regular 54px.
4. **Dashboard centering** — Changed from CSS grid to flexbox. Stat blocks are 130px wide (matching Figma's 130px center-to-center spacing). Left specs 200px, right amenities 180px.
5. **Video Call Now button** — Applied Inter Semi Bold 26px, letter-spacing -1.04px, uppercase.
6. **Font audit** — Updated country tabs (Inter Light 16px, -0.64px tracking), spec labels (letter-spacing 0.84px), CTA sub-buttons (Inter Medium 20px, -0.8px tracking).
7. **Progressive blur on yacht name area** — Implemented using CSS `mask-image` gradient on `backdrop-filter: blur(12px)`. Blur gradually appears from top to bottom (transparent → opaque mask).
8. **Carousel transitions** — Added crossfade animation for main yacht image (300ms fade-out → swap → 500ms fade-in). Side images have CSS transitions for position/size/opacity. Navigation blocked during animation to prevent rapid-fire.

### 2026-03-13 — Session 2: Audit Fix Pass

**Figma vs build audit — fixes applied:**

1. **Side images 3D perspective** — Added `perspective(1200px) rotateY(±6deg)` to side images, `±10deg` for far images. Images now tilt toward the card like in Figma.
2. **Frosted header tighter** — Reduced padding from `30px 30px 20px` to `20px 30px 16px`. Picker repositioned to `top: 72px`.
3. **Yacht name area compact** — Reduced from 200px to 160px height. Blur mask tightened (20%→80% fade). Less dark overlay.
4. **Dashboard compact** — Padding reduced to `20px 40px 16px`. Spec row line-height 1.8→1.6. Stat label margin 8→4px. Amenity line-height 1.6.
5. **CTA padding reduced** — `8px 4px 10px` → `4px 4px 8px`.
6. **Turkish characters** — Fixed İnternet, Duş, consolidated Knee/Kano/Jetski into one line.
7. **Overall card height** — All padding reductions result in a more compact card matching Figma proportions.

### 2026-03-13 — Session 2: Progressive Blur + CTA Fix

1. **Progressive blur (yacht name area)** — Replaced uniform `backdrop-filter` with two-layer approach: `::before` layer has `backdrop-filter: blur(10px)` with CSS `mask-image` gradient (transparent top → opaque bottom) for true progressive blur. `::after` layer has `rgba(0,0,0,0.3)→transparent` dark gradient overlay. Matches Figma's "Frost Blur" node exactly.
2. **CTA button clickable** — Added `pointer-events: none` on `.cta-subs` container, `pointer-events: auto` on individual sub-buttons. Main button now clickable in center area. Enhanced hover (`translateY(-2px)`, brighter `#00d9cc`, glow intensifies) and active (`scale(0.995)`, darker `#00bfb3`) states. Sub-buttons get `scale(1.02)` on hover.
3. **Yacht name positioning** — Decorative asset `margin-bottom: -8px`, name `margin-bottom: 12px` for tighter Figma-accurate spacing.

### 2026-03-13 — Session 2: Alignment + Blur + Header Fix

1. **Yacht name area rebuilt with CSS** — Replaced Figma decorative asset image with pure CSS/SVG: SVG chevron (24x14px, `stroke-width: 2`) 10px above name. Two 110px horizontal lines at 99px from card edges, baseline-aligned with yacht name text. Bottom margin 14px.
2. **Real progressive blur** — Three stacked `backdrop-filter` layers with masked gradients: Layer 1 (2px blur, full height), Layer 2 (4px blur, bottom 70%), Layer 3 (8px blur, bottom 40%). Each layer uses `mask-image: linear-gradient(to bottom, transparent, black)` for true progressive blur. Dark gradient overlay `rgba(0,0,0,0.35)` → transparent via `::after`.
3. **Frosted header restored to 180px** — Single frosted area covers both country tabs AND month slider. Picker moved back inside frosted-header div. Picker uses `width: calc(100% + 60px); margin: 0 -30px` to extend edge-to-edge within the header.
4. **CTA pointer-events fix** — `.cta-subs` container set to `pointer-events: none`, individual sub-buttons to `pointer-events: auto`. Main button now receives clicks in center area.

### 2026-03-13 — Session 3: Carousel → Picker Rewrite + Local Assets

**Problem:** Slide-based carousel had poor UX — felt like a slider, not a selector. User requested the same picker pattern used by the month slider (drag/snap/infinite-scroll).

**Changes:**

#### Yacht Picker (complete rewrite)
1. **Picker-style navigation** — Replaced slide carousel with `createYachtPicker()` modeled on `createMonthPicker()`. Same drag/snap physics, infinite scroll (5 copies), distance-based opacity/scale.
2. **Distance-based styling** — Opacity: `[1, 1, 0.6, 0.3, 0.1]` by distance from center. Scale: `dist===1: 1, dist===2: 0.88, else: 0.75`.
3. **Selected item** — Width `920px` (matches card), `opacity: 0`, `pointer-events: none`. Side items `340px` wide.
4. **Click navigation fixed** — Refactored pointer handling: drag mode only activates after 5px movement threshold. Pure clicks pass through cleanly to the click handler which snaps picker to clicked yacht.
5. **Side thumbnail labels removed** — `createYachtItem()` no longer creates label divs. Only the main card shows the yacht name.
6. **Wheel navigation** — Mouse wheel on picker area navigates between yachts.
7. **Keyboard navigation** — Arrow left/right keys navigate between yachts.

#### Cross-dissolve Image Transition
8. **True cross-dissolve** — Two stacked `<img>` layers (A/B) alternate. New image fades to `opacity:1` while old fades to `opacity:0` simultaneously (`transition: opacity 0.5s ease`). Replaced old sequential fade-out/delay/fade-in approach.

#### Local Assets & Project Organization
9. **Project folder created** — `SpecialProjects/NavigaYachting/` with `assets/` subfolder.
10. **All images downloaded locally** — 18 yacht images in `assets/yachts/`, flags in `assets/flags/`, logo in `assets/`.
11. **All image paths updated** — From remote URLs to local `assets/yachts/*.jpg`, `assets/flags/*.png`, `assets/logo.svg`.
12. **Logo fix** — File was SVG content saved as `.png` extension. Renamed to `logo.svg` so browsers render it correctly.

#### CTA Fix
13. **CTA padding equalized** — Bottom-left, bottom-right, and bottom now share equal `4px` padding.

### 2026-03-13 — Session 2: Layout & Spacing Final Pass

1. **Main card vertical centering** — Changed `.page` from `align-items: flex-start` to `align-items: center` with `padding: 20px`. Card now always vertically centers on the viewport regardless of screen height.
2. **Frosted header vertical spacing** — Increased `.frosted-header` gap from `12px` to `18px` to push month slider slightly lower within the 180px frosted area. Better visual breathing room between country tabs and month picker.
3. **Yacht visual area reduced** — `.yacht-visual` height reduced from `637px` to `560px`. Dashboard area no longer appears squeezed; better proportion balance between image and info sections.
4. **Yacht name area blur removed** — Completely removed all `backdrop-filter`, `::before` blur layers, and `::after` dark overlay from `.yacht-name-area`. User will design this effect separately. Clean transparent overlay now.
5. **Picker edge-fade gradients removed** — Removed `::before` and `::after` pseudo-element gradients from `.picker-wrapper` that were causing visible gradient duplication on the frosted header. Distance-based opacity on picker items (±1=1.0, ±2=0.70, ±3=0.30, ±4=0.10) already handles visual fading without edge masks.

### 2026-03-13 — Session 4: Carousel Depth Effect + Header Padding Fix

**Carousel depth effect:**
1. **Scale + opacity by distance** — Restored carousel "depth feeling" with progressive scale-down and opacity fade. `distScale = [1, 0.92, 0.82, 0.72, 0.62, 0.55]`, `distOpacity = [1, 1, 0.7, 0.4, 0.15, 0.05]`. Items further from center appear smaller and more transparent.
2. **Removed negative margins** — Initial attempt used negative margins (`margin: 0 -gap`) to make scaled items flush/touching. This broke `getTranslate()` centering math (assumed uniform `smallWidth` layout) and pushed carousel items off-viewport. Fix: removed all negative margin logic, relying on `transform: scale()` alone (purely visual, doesn't affect layout). Items have small visual gaps but positioning is correct.
3. **Carousel item sizing** — Thumbnails are 150×240px (10:16 aspect ratio), `border-radius: 12px`. Selected item expands to 920px width (hidden behind main card).
4. **Full viewport width** — Picker wrapper is `position: fixed; width: 100vw; left: 0` so carousel extends to browser edges.
5. **Dynamic vertical alignment** — JS `alignPicker()` calculates exposed image center (below 180px frosted header) and positions carousel wrapper accordingly. Recalculates on window resize.
6. **Navigation arrows** — Left/right frosted glass buttons (`rgba(0,0,0,0.25)` + `backdrop-filter: blur(8px)`) on main card image, shown on hover. Positioned at `top: 66%` to align vertically with carousel thumbnails.

**Header padding fix (Figma match):**
7. **Top padding** — `.frosted-header` padding-top changed from `20px` to `30px` (Figma: tabs start 30px from card top).
8. **Tab gap** — `.country-tabs` gap changed from `10px` to `20px` (Figma: 20px between 200px-wide tabs).
9. **Tabs→picker gap** — `.frosted-header` gap changed from `18px` to `22px` (Figma: 22px between bottom of tabs and top of month picker).

### 2026-03-27 — Session 5: Adaptive Design (Desktop → Tablet → Mobile)

**Figma frames used:**
- `Homepage - Main` (35:252, 1920×1080) — desktop reference
- `Homepage - Mobile - Main` (78:292, 440×956) — mobile reference

**Breakpoints:** Desktop (>1024px) · Tablet (601–1024px) · Mobile (≤600px)

#### Structural — Mobile adaptive layout
1. **Card shell removed on mobile** — `.main-card` loses background, shadow, border-radius. Content flows on white page. `display: contents` on `.yacht-visual` explodes the image container so frosted-header, image, name, dashboard, and CTA become direct flex children.
2. **Sticky header** — Logo + country tabs + month picker stick to top via `position: sticky; top: 0` on `.frosted-header` inside the scrollable `.main-card`. Logo positioned absolutely over the gradient header area.
3. **Sticky CTA footer** — CTA area uses `position: sticky; bottom: 0; margin-top: auto` to always pin at the bottom of the viewport.
4. **Scrollable middle** — `.main-card` becomes `overflow-y: auto; flex: 1` so the yacht image, name, and dashboard scroll between the sticky header and footer.
5. **Mobile gradient header** — Gradient background (`113.36deg, #d1fefb → #f7fffe`) applied directly to `.frosted-header` instead of a separate fixed div.

#### Components — Mobile style changes
6. **Country tabs** — Inverted: black borders, black text, 100px pills, no flag icons. Active = black fill + white text. Gap: 6px, left-aligned at `padding-left: 11px`.
7. **Month slider** — Black text on light background. Selected item gets `box-shadow: 0px 10px 30px rgba(0,0,0,0.3)`. Selected card overlaps yacht image by 8px (`margin-top: -8px` on image) matching Figma positioning.
8. **Yacht image** — 230px tall, `border-radius: 20px`, 20px horizontal margin. Dark gradient overlay removed. Cross-dissolve uses `data-current` attribute to show active layer only.
9. **Nav arrows** — 36×36px, always visible, positioned at `left: 15px / right: 15px`. JS `alignMobileNavArrows()` calculates vertical center relative to active image. MutationObserver re-positions on yacht change.
10. **Yacht name** — New mobile-only element (`#yachtNameMobile`) below image. Black text, 32px EB Garamond SemiBold, 60px decorative lines. JS syncs both desktop and mobile name elements.
11. **Dashboard** — Two-row layout: stats (3× 120px blocks, gap: 10px) on top row, specs (170px) + vertical divider + amenities (170px) side-by-side below. Gap: 30px total between specs/amenities.
12. **CTA** — Two-row: "Video Call Now" centered on top, horizontal divider, "Watch Video" | vertical divider | "Call Me" below. Golden gradient (`#ffb366 → #ffdc8c`), `border-radius: 20px`.

#### Tablet (601–1024px)
13. **Card fluid** — `width: 100%; max-width: 920px`. Carousel and watermark hidden. Nav arrows always visible.
14. **Frosted header** — `overflow: hidden` clips month picker within card bounds. Tighter padding and 160px tabs.
15. **Dashboard** — Horizontal layout preserved with tighter gaps (30px), smaller stat numbers (40px), narrower specs (150px).

#### Cross-cutting fixes
16. **Image crossfade fix** — `currentImg.removeAttribute('data-current')` after swapping layers. Prevents both images showing simultaneously on mobile where CSS `!important` overrides inline opacity.
17. **Month picker resize fix** — `wrapperCenter` was calculated once at init, causing misaligned items when resizing between breakpoints. Now recalculates via `resize` event listener and re-snaps track position.
18. **CTA button text** — "Schedule" renamed to "Call Me" matching updated Figma design.

### 2026-03-27 — Session 5b: Mobile Layout Zones + Pixel-Perfect Pass

**Zone architecture defined:**
```
┌─────────────────────────────────┐
│  ZONE A — STICKY HEADER         │ ← sticky top, gradient bg
│  Logo + Tabs + Month Picker     │
├─────────────────────────────────┤
│  ZONE B — SCROLLABLE CONTENT    │ ← flex:1, overflow-y:auto
│  Image (fixed 230px) + Name     │
│  Stats + Specs (stretches)      │
├─────────────────────────────────┤
│  ZONE C — STICKY FOOTER         │ ← sticky bottom, gold gradient
│  Video Call Now / Watch / Call   │
└─────────────────────────────────┘
```

**Changes:**
1. **Three.js bg kept on mobile** — removed separate `mobile-gradient-header` div. Desktop's Three.js canvas + gradient stays visible through mobile layout. Zone A header has its own gradient overlay.
2. **Yacht image fixed ratio** — `height: 230px !important; flex: 0 0 230px` prevents image from stretching. `aspect-ratio` approach failed due to flex container interference.
3. **Dashboard stretches** — `flex: 1 0 auto` on `.dashboard` makes the Name + Stats + Specs zone fill remaining vertical space between image and CTA.
4. **Zone C border-radius** — Changed from `border-radius: 20px` (all corners) to `20px 20px 0 0` (top corners only) since it sits flush at viewport bottom.
5. **Figma-exact paddings** — Zone A: `padding: 48px 11px 0` (room for logo). Zone B image: `margin: -8px 20px 0`. Dashboard: `padding: 0 35px 10px`. CTA: `padding: 24px 20px 20px`.

---

## Reference Files

| File | Purpose |
|------|---------|
| `index.html` | **Main deliverable** (single HTML file, inline CSS + JS, local assets) |
| `assets/` | Local images: `yachts/`, `flags/`, `logo.svg` |
| This document | Project tracker |
