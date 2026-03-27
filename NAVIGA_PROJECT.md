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

### 2026-03-27 — Session 6: Logo Aspect-Ratio Fix + Z-Index + Mobile Logo

**Logo SVG fix:**
1. **SVG intrinsic dimensions** — `logo.svg` had `preserveAspectRatio="none"` and `width="100%" height="100%"`, causing the logo to stretch/squash to fill its container at non-1920px widths. Fixed: `preserveAspectRatio="xMidYMid meet"`, `width="184" height="71"` (matching viewBox).
2. **CSS height: auto** — Both `.logo` and `.logo img` changed from fixed/percentage `height` to `height: auto`, so the SVG's natural 184:71 ratio is always preserved across all breakpoints.

**Logo z-index — pushed to background:**
3. **Desktop z-index** — `.logo` changed from `z-index: 20` to `z-index: 1`. Logo now renders behind the card, carousel, and all interactive UI.
4. **Tablet z-index** — Same `z-index: 1` in the ≤1024px breakpoint.

**Mobile logo — visible per Figma:**
5. **Logo restored on mobile** — Changed from `display: none` to `display: block; position: fixed; top: 12px; left: 11px; width: 77px; z-index: 30`. Matches Figma "Homepage - Mobile - Main" (78:292) where logo sits top-left at 77×30px.
6. **Header padding** — Frosted header `padding-top` kept at `48px` to accommodate logo above country tabs.

**Month picker edge-to-edge fix:**
7. **Picker width on mobile** — Changed from `width: 100%; margin: 0` to `width: calc(100% + 22px); margin: 0 -11px` so the month picker extends to screen edges past the frosted header's `11px` padding.

### 2026-03-27 — Session 6b: Mobile Yacht Image Crossfade Layout Fix

**Problem:** On mobile, yacht images would sometimes stretch to full width and sometimes not when switching yachts. Root cause: the two crossfade image layers (A/B) used CSS `:nth-of-type(2)` to make only the second image `position: absolute`. When crossfade swapped the active layer, both images could momentarily be `position: relative` flex participants, causing the row to expand unpredictably.

**Fix — `.yacht-img-wrap` container:**
1. **New wrapper div** — Added `.yacht-img-wrap` around `imgA` + `imgB`. On desktop: `display: contents` (invisible, no layout impact). On mobile: `display: block; position: relative; flex: 1 1 auto; overflow: hidden; border-radius: 20px`.
2. **Both images always absolute** — Removed `:nth-of-type(2)` and `[data-current]` layout-switching approach. Both `.yacht-visual-img` elements are now always `position: absolute; inset: 0` inside the wrapper on mobile. The wrapper is the single stable flex participant between the peek images.
3. **Stable layout** — The wrapper maintains a fixed flex slot between the two 40px carousel peeks. Crossfade only toggles `opacity` and `z-index` on the images — no position/flex changes, so no layout shift.

### 2026-03-27 — Session 6c: Mobile Yacht Image Spacing + Corners

**Figma reference:** Image at `top: 190px`, `400×230px` centered in 440px frame, `border-radius: 20px` all corners. No frosted overlay — gradient background sits above, image starts cleanly below.

**Fixes:**
1. **Removed image overlap** — `margin-top: -8px` → `margin-top: 0` on `.yacht-image-row`. Image no longer tucks under the header gradient.
2. **Header spacing** — `.main-card` `padding-top: 160px` → `190px` to match the Figma gradient area height (190px). Image starts right where the gradient ends.
3. **Image horizontal margins** — Added `padding: 0 20px` on `.yacht-image-row` so the image is 20px inset from screen edges, matching Figma's 400px image in 440px frame.
4. **All-corner radius** — `.yacht-img-wrap` already has `border-radius: 20px; overflow: hidden`, giving all four corners the 20px radius per Figma.

### 2026-03-27 — Session 7: Dashboard Figma Audit (Desktop + Mobile)

**Figma MCP verification** — Pulled design context for both `Homepage - Main` (35:252) and `Homepage - Mobile - Main` (78:292). Compared "Selected Yacht: Dashboard" node parameters against current implementation.

**Fixes:**
1. **Mobile stat-number font-size** — At `≤600px`, the tablet media query (`max-width: 1024px`) also applies and had reduced `.stat-number` to `40px`. Mobile section now explicitly resets `.stat-number { font-size: 48px }` to match Figma mobile frame.
2. **Mobile dashboard row distribution** — Dashboard had `flex: 0 0 auto; align-content: flex-start`, packing both rows (stats, specs/amenities) to the top. Changed to `flex: 1 1 0; align-content: space-evenly` so the two wrapped rows distribute vertically within the available space between yacht name and CTA footer, respecting padding rules.

### 2026-03-27 — Session 7b: Contact Panel ("Button Clicked - Live")

**Figma frames used:**
- `Homepage - Button Clicked - Live` (62:2, 1920×1080) — desktop reference
- `Homepage - Mobile - Button Clicked - Live` (78:815, 440×956) — mobile reference

**Feature:** Clicking "Video Call Now" or "Call Me" opens a golden contact panel overlay inside the main card.

#### Architecture
- **Overlay approach** — New `div.contact-panel` positioned absolutely inside `.main-card` (desktop) or `position: fixed` (mobile). Normal card state preserved underneath for instant restoration.
- **Animation** — `translateY(100%)` → `translateY(0)` with `cubic-bezier(0.23, 1, 0.32, 1)` over 500ms. Golden gradient matches CTA bar for visual continuity ("CTA expands upward"). Children stagger in with 60ms delays.
- **Close** — X button on image (both), "Go to Back" button (desktop only), Escape key. Yacht arrow navigation disabled while panel is open.

#### Desktop layout
1. **Yacht image** — Compressed to 200px height (from 637px), gradient overlay + yacht name preserved.
2. **White header** — "Connect with" (Inter Bold 24px) + "*the crew*" (EB Garamond SemiBold Italic 54px) + description. X close button at top-right.
3. **Contact cards** — 2-column grid + 1 full-width: WhatsApp, FaceTime, Google Meet, Phone Call, Schedule a Call. Each 110px tall, `bg-rgba(255,255,255,0.2)`, `rounded-20px`, 60px icon circle, chevron arrow.
4. **Bottom bar** — "Go to Back" button (190×73px, white/40%) + live status bar with indicator icon.

#### Mobile layout
5. **Yacht image** — 170px height, full-width, no border-radius.
6. **Cards stacked** — Single column, 90px tall each (Schedule: 110px). Titles 18px, subtitles 13px.
7. **No "Go to Back"** — X close button serves that role.
8. **Live bar** — Full-width at bottom, 13px text.

#### Technical
9. **Font import** — Added EB Garamond italic variant (`ital,wght@...;1,600`) for "the crew" text.
10. **Inline SVG icons** — WhatsApp, FaceTime, Google Meet, Phone, Calendar, Live indicator, Close (X), Chevron. No external icon dependencies.
11. **Scroll preservation** — Mobile saves/restores `.main-card` scrollTop when opening/closing panel.
12. **Keyboard** — Arrow key navigation blocked (capture phase `stopImmediatePropagation`) while panel is open.

### 2026-03-27 — Session 7c: Contact Panel Fixes (Icons, Offline, Close Button, CSS)

**Figma frames added:**
- `Homepage - Button Clicked - Offline` (78:196, 1920×1080) — desktop offline
- `Homepage - Mobile - Button Clicked - Offline` (78:984, 440×956) — mobile offline

**Fix #1 — Real icon assets from Figma:**
- Downloaded 8 icons to `assets/icons/`: `whatsapp.svg`, `facetime.svg`, `googlemeet.svg`, `phone.png`, `calendar.png`, `live.png`, `close.svg`, `chevron.svg`
- Replaced all hand-drawn inline SVGs with `<img>` tags pointing to real Figma raster/vector assets

**Fix #2 — Offline state:**
- Added `.contact-panel.offline` CSS class with Figma-exact disabled card styles:
  - Card bg: `rgba(210,163,104,0.2)`, icon bg: `rgba(255,255,255,0.1)`
  - Title opacity: 0.4, subtitle opacity: 0.1, no chevrons, `pointer-events: none`
  - Phone Call icon extra `opacity: 0.2`
- Schedule a Call stays active (different bg/icon styling, keeps chevron)
- JS `crewIsLive` flag toggles between states: changes description text, live bar text, schedule title
- Offline description: "The crew is currently off board. Schedule a call - they'll reach out to confirm a time."
- Offline bottom bar: "Leave a message and they'll get back to you **as soon as possible.**"
- Schedule title changes to "Schedule a Call / Call me later" in offline mode

**Fix #3 — X close button placement:**
- Desktop: X only in white header area (`.contact-header-close`), positioned `top: 24px; right: 40px` using `close.svg` icon
- Mobile: X only on yacht image (`.contact-close-mobile`), hidden on desktop via `display: none`
- Added separate CSS class `.contact-close-mobile` to distinguish the two buttons

**Fix #4 — White header 187px:**
- Added `min-height: 187px` and `display: flex; flex-direction: column; justify-content: center` to `.contact-header`
- Mobile override resets `min-height: auto`

**Fix #5 — Go to Back border-radius:**
- Changed from `12px 20px 20px 12px` to `0 20px 20px 12px` — top-left is flush with card edge per Figma

**Fix #6 — Live icon sizing:**
- `.contact-live-icon` set to `50×50px` with `border-radius: 4px; object-fit: cover` matching Figma's 50×50 live indicator

### 2026-03-27 — Session 7d: Contact Panel Polish Pass

**Fixes applied from review feedback:**

1. **X close specificity** — `.contact-close-btn.contact-close-mobile { display: none !important }` ensures desktop hides the image X even though `.contact-close-btn` has `display: flex`.
2. **Live icon sizing** — HTML `width/height` attributes changed from 24 to 50 to match CSS. Mobile override added: `width: 24px; height: 24px; border-radius: 4px`.
3. **Carousel repositioning** — `.yacht-picker-wrapper.panel-active` class added with `pointer-events: none` and smooth transition. JS in `openContactPanel()` calculates carousel center as midpoint of golden content area below the white header. `closeContactPanel()` removes class and re-runs `alignPicker()`.
4. **Contact options bottom padding** — Changed from `10px 40px 0` to `10px 40px 20px` for proper spacing before bottom bar.
5. **CTA data attributes** — Added `data-cta="videocall|callme|watch"` to all CTA buttons. JS now uses `[data-cta="videocall"], [data-cta="callme"]` selector instead of fragile `textContent.trim()` matching.
6. **applyCrewState() stale DOM** — Restructured live bar HTML with `#contactLiveBold`, `#contactLiveDetail`, `#contactLiveYacht` spans. Live state updates text nodes directly. Offline state still uses innerHTML for the different message structure but re-queries from DOM.
7. **Frosted glass effects** — Added `backdrop-filter: blur()` + `-webkit-backdrop-filter: blur()` to all semi-transparent elements:
   - Contact cards: `blur(12px)`
   - Icon containers: `blur(8px)`
   - Go to Back button: `blur(10px)`
   - Live status bar: faked glass

### 2026-03-27 — Session 7e: Contact Panel Bug Fixes (11 items)

1. **Duplicate var** — Removed second `var contactLiveYacht` declaration.
2. **Offline innerHTML** — Replaced with dedicated `#contactOfflineMsg` span. `applyCrewState()` now toggles `display` on `#contactLiveDetail` and `#contactOfflineMsg` — no more innerHTML rebuilding, no stale DOM references.
3. **Mobile close button (CRITICAL)** — Removed `!important` from desktop hide rule. Scoped to `@media (min-width: 601px) { .contact-close-mobile { display: none } }`. Mobile `@media` override now works correctly.
4. **Carousel → static side images** — Replaced `.panel-active` carousel repositioning with two new static `<img>` elements (`.panel-side-left`/`.panel-side-right`) inside `.page-inner`. Figma: 328×421px at ±316px from card center, 198px from card top. JS `showPanelSideImages()` sets src from prev/next yachts in current list, positions with absolute coords relative to card. Scrolling carousel hidden via `display: none` while panel is open. `hidePanelSideImages()` restores carousel and re-runs `alignPicker()`.
5. **Carousel CSS** — Removed `.yacht-picker-wrapper.panel-active` (unused). Added `.panel-side-img` with `328×421px, border-radius: 20px, object-fit: cover, opacity transition`.
6. **Offline dimmed cards** — Removed `backdrop-filter: none`, changed to `border-color: rgba(210,163,104,0.15); box-shadow: none` for subtle brown-tinted glass.
7. **Close inline styles** — `hidePanelSideImages()` uses `pickerWrapper.style.display = ''` (clear) then `alignPicker()`. No lingering inline styles.
8. **Watch Video** — No handler (noted, not in scope of contact panel).
9. **Scrollbar hidden** — Added `scrollbar-width: none` + `.contact-panel::-webkit-scrollbar { display: none }`.
10. **Glass effects** — Replaced all `backdrop-filter: blur()` with faked glass: `background: rgba(255,255,255,0.25); border: 1px solid rgba(255,255,255,0.3); box-shadow: 0 2px 16px rgba(0,0,0,0.06), inset 0 1px 0 rgba(255,255,255,0.4)`. Works on flat gradient backgrounds where real blur has no visible effect.
11. **Static side images** — See #4 above.

---

### 2026-03-27 — Session 7f: Side Image Animation + Mobile Contact Panel Fixes

**Side image animation polish:**
1. Base state changed from `display: none; opacity: 0` to `display: block; opacity: 0; pointer-events: none` — opacity transition now fires correctly on show.
2. `hidePanelSideImages()` removes `.visible` class (opacity → 0), then restores carousel after 500ms timeout to let fade-out complete.

**Mobile contact panel — Figma pixel match:**
3. **White header zone** — Mobile `.contact-panel` background changed from golden gradient to `#fff`. Golden gradient moved to `.contact-options` background on mobile, matching Figma where gradient starts at card area (`top: 341px`). `.contact-bottom` gets solid `#ffb76d`.
4. **Header padding** — Changed from `16px 20px 12px` to `36px 20px 14px` matching Figma: "Connect with" at 35.5px below image, first card at ~326px from top.
5. **Header background** — `background: #fff` on mobile (was `transparent`), giving the text area a white zone before the golden cards.
6. **X close button** — Changed from 36×36px circle at `top: 14px; right: 14px` to bare 20×20px icon at `top: 50px; right: 40px` matching Figma Union icon placement. No background, no border-radius.

### 2026-03-27 — Session 7g: Mobile Padding Pixel-Exact Pass

**Figma reference:** `Homepage - Mobile - Main` (78:292, 440×956)

All changes in `@media (max-width: 600px)` only — desktop/tablet unaffected.

1. **Logo** — `top: 12px; left: 11px` → `top: 20px; left: 20px` (Figma node 78:1049)
2. **Frosted header** — `padding: 48px 11px 0` → `56px 11px 0` (accommodates logo shift: 20px top + 30px height + 6px gap)
3. **Main card padding-top** — `184px` → `192px` (matches new header height)
4. **Yacht name area** — `padding: 16px 40px 0` → `20px 40px 0` (Figma: ~20px below image)
5. **Dashboard** — `padding: 0 35px 10px` → `0 40px 10px` (Figma: specs start ~40px from edge)

---

## Reference Files

| File | Purpose |
|------|---------|
| `index.html` | **Main deliverable** (single HTML file, inline CSS + JS, local assets) |
| `assets/` | Local images: `yachts/`, `flags/`, `logo.svg`, `icons/` |
| `assets/icons/` | Contact panel icons: `whatsapp.svg`, `facetime.svg`, `googlemeet.svg`, `phone.png`, `calendar.png`, `live.png`, `close.svg`, `chevron.svg` |
| This document | Project tracker |
