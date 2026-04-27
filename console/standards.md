# LESARUSS Standards

**Updated:** 2026-04-17

---

## ADA / Accessibility (WCAG 2 AA - Mandatory)

Run the ADA check on EVERY visual output before delivery. No exceptions.

### Color Contrast (4.5:1 minimum normal text, 3:1 large text)

**Light Theme - Passing:**
| Foreground | Background | Ratio | Use |
|-----------|-----------|-------|-----|
| #1A1A1A | #ffffff | 18.1:1 | Primary text |
| #555555 | #ffffff | 7.0:1 | Secondary text |
| #767676 | #ffffff | 4.54:1 | Muted text (minimum) |
| #F69820 | #1A1A1A | ~8:1 | Orange on dark only |

**FAILS:** Orange #F69820 on white = 2.22:1. Never use orange text on light backgrounds.

**Dark Theme - Passing:**
| Foreground | Background | Ratio | Use |
|-----------|-----------|-------|-----|
| #e0e0e0 | #111111 | 14.3:1 | Primary text |
| #aaaaaa | #1A1A1A | 7.5:1 | Secondary text |
| #999999 | #2a2a2a | 5.0:1 | Muted text on card |

**FAILS:** #666666 on dark backgrounds (~3.3:1). #888888 on #2a2a2a = 4.05:1.

### CSS Variables (locked)
- --dir-text-muted: #767676 (light), #999999 (dark)
- --dir-text-secondary: #555555 (light), #aaaaaa (dark)
- --dir-text: #1A1A1A (light), #e0e0e0 (dark)

### Heading Order
h1 > h2 > h3, no skipping levels. Eyebrow labels use <p>, not headings.

### Interactive Elements
- <button> for actions, <a href> for navigation, never <div onclick>
- Focus rings: outline 3px solid #F69820, outline-offset 3px
- Always include prefers-reduced-motion for animations

### iOS Safari
Input font-size must be 16px minimum (prevents auto-zoom on focus).

---

## Internal Page Template (LOCKED Apr 15)

Before creating ANY internal HTML page:
1. Copy _templates/internal-page-LOCKED.html
2. Only edit content inside <main> marked EDIT BELOW
3. Never hand-write nav/drawer/footer/CSS variables

**Top bar:** 62px fixed, backdrop blur. Left: LESARUSS.AI wordmark with pulsing dot. Right: 32px module icons + SR avatar.
**Left drawer:** Pulsing toggle at left edge, opens 300px nav drawer. Links: Mission Control, Brand, Directory, Library, Playbooks, Modules, Settings.
**Theme:** White-only universal default (LOCKED 2026-04-24). Every surface defaults to white background. Dark mode is an opt-in module the user enables, never a time-of-day auto-switch. Strip any auto-theme JavaScript on edit. See `console/locked-rules.md` section 2.1.
**Footer:** LESARUSS.AI mark + nav links + copyright.

---

## Design System

**Public template:** 62px fixed nav. Left: LESARUSS. wordmark + inline links. Right: theme toggle + Login + Enter CTA.
**Project/Internal template:** 58px fixed nav. Same two-shell architecture (public = one shell, project+internal = one shell).
**Cards:** Flip card module, 3D Y-axis flip, 4 columns desktop.
**Wordmark:** LESARUSS<span class="dot">.</span> with orange period, not dot circle.

---

## Working Style

- Handle tasks directly and automatically. Minimize manual steps for Sean.
- Before pushing code or deploying, show a visual mock for approval first.
- All mocks must include desktop/tablet/mobile viewport switcher with orange pull handle.
- Never use terminal for git push. Use Chrome MCP GitHub API.
- All reports and briefs must be HTML (never .md as deliverable).
- Every amended report needs a "What Changed" panel at top.
- Every internal HTML doc auto-pushes to `public/<same-path>/` on `main` in the same turn (LOCKED 2026-04-24).
- Every non-trivial public-page change ships to `public/v<N>/index.html` first for review, then is ported to the routed page (LOCKED 2026-04-24).
- Every page must point to a next action. No dead-end pages. List pages need per-card CTAs (LOCKED 2026-04-24).
- White background is the universal default. Dark mode is opt-in only (LOCKED 2026-04-24).
- LESARUSS-owned brand pages do not include a claim rail. Claim rails appear only on third-party listings (LOCKED 2026-04-26).
- Vercel-deployed commits are authored as `Sean A. Russell <contact@lesaruss.com>`. Never `claude@lesaruss.ai` (LOCKED 2026-04-25). See `console/deploy.md`.
- For the full master index of every locked universal rule, see `console/locked-rules.md`.
