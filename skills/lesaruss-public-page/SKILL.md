---
name: lesaruss-public-page
description: >
  LESARUSS public HTML/TSX page guardrail. USE THIS SKILL automatically
  whenever creating, editing, or rewriting any page that lives on a public
  surface of the LESARUSS universe (lesaruss.ai, project.lesaruss.com,
  brand subdomains). Triggers on: "build a public page", "new public route",
  "intake", "welcome", "claim", "contact", "about", "brands", "leaderboard",
  "case studies", "media", "/c/<slug>", "front door", PublicNav, PublicFooter.
  Also triggers when a file path matches `app/(public)/**`, `components/public/**`,
  or `public/v<N>/**` inside the lesaruss-project repo. Never hand-write the
  PublicNav, PublicFooter, eyebrow, or hero. Place the route inside the
  `(public)` route group so the locked shell wraps it automatically. The same
  drift correction has already cost multiple round trips with Sean. This
  skill prevents the next.
---

# LESARUSS Public Page Template, Pre-Flight Guardrail

Run this before writing any public-facing TSX or HTML inside the lesaruss-project repo.
The locked shell already exists, already passes WCAG 2 AA, already carries the
correct nav, footer, font, and dot pulse. Hand-rolled public pages drift, drift
costs round trips, and this skill prevents that.

---

## 1. Read the source of truth first

Before you write anything, read these files in order from your `~/Code/lesaruss-project` clone (or a fresh `/tmp/<short>` clone if that station has not been provisioned per rule 4.5):

1. `app/(public)/layout.tsx`, the locked route-group shell
2. `components/PublicNav.tsx`, the canonical top nav
3. `components/PublicFooter.tsx`, the canonical footer
4. `components/public/PageHero.tsx`, display hero
5. `components/public/PageHeroCompact.tsx`, form-page hero
6. `components/public/MemberBanner.tsx`, "already a member" skip box
7. `app/(public)/intake/page.tsx`, the canonical reference page (multi-step form pattern)

If any of those files are missing on your station, stop and pull. Do not hand-write a substitute.

---

## 2. Place the new page inside the (public) route group

Every public-facing page lives at `app/(public)/<route>/page.tsx`. The route URL is unchanged. The route group exists so the locked shell wraps every page automatically.

- Do NOT place a public page at `app/<route>/page.tsx` directly. That bypasses the lock.
- Do NOT import `PublicNav` or `PublicFooter` inside the page body. The (public) layout already renders them.
- Do NOT define a custom `<main>` wrapper. The (public) layout already provides one with `padding-top: 62` to clear the fixed nav.
- Do set route-specific `metadata` via the standard Next.js export. The route group's `metadata` defines the title template.

---

## 3. Use the locked hero family

For any page where the first surface is a title block, use one of:

- `<PageHero eyebrow title subtitle />`, the display hero (max-width 1100, eyebrow at #555 on white = 7.5 to 1)
- `<PageHeroCompact eyebrow title subtitle />`, the form hero (max-width 720, integrates with progress bars)

Never roll your own h1 + eyebrow + lead block. The hero family already passes AA, owns the typography, and locks the eyebrow color so the orange-on-white contrast bug never reappears.

---

## 4. Wordmark, font, color rules

- Wordmark on every public page is `LESARUSS.AI` with the pulsing dot accent. The legacy `LESARUSS PROJECT` treatment is retired.
- Font is Montserrat, weights 200, 300, 400, 500, 700, 800, 900, loaded by the root layout via `next/font/google`. Do NOT hand-import Google Fonts in a public page.
- Background is white (`var(--lr-bg)`). Dark mode is a member-only module, never a default for public surfaces (rule 2.1).
- Orange `#F69820` is reserved for non-text accents (dot pulse, progress fill, banner left-rule, primary CTA background, leaderboard your-row highlight). Orange text on white fails AA (2.22 to 1). Never use orange text on white for body or eyebrow type.
- Body type uses `--lr-text-75`, eyebrow uses `--lr-text-50`, headings use `--lr-text`.

---

## 5. Mock-to-prod preview before promoting

Per rule 1.3, every non-trivial public page change ships first to `public/v<N>/<route>/index.html` as a static preview, gets reviewed on real Vercel infra by Sean, and only then promotes into the routed `app/(public)/<route>/page.tsx`. Do NOT push straight to live without a v-preview pass.

The current locked example is `public/v1/intake/index.html`, the static preview that mirrors the routed page at `app/(public)/intake/page.tsx`. Every drift between the two is a bug.

---

## 6. ADA AA mandatory

Every public page passes WCAG 2 AA before Sean sees it. Run the check silently, deliver a one-line summary. Locked checks for the public surface:

- Eyebrow color is `var(--lr-text-50)` on white, never orange.
- Required-field asterisks are visible (`*`) AND the input carries `aria-required="true"`. The asterisk is hidden from screen readers via `aria-hidden`.
- Conditional reveal blocks use `aria-live="polite"` so the new fields are announced.
- Progress bar uses `role="progressbar"` with `aria-valuenow` updated on each step.
- Focus rings visible on every interactive element. Tab order follows visual order.
- Em-dashes are not used anywhere. Commas, periods, colons, plain hyphens only.
- Buttons that toggle state expose `aria-pressed`. Modal triggers expose `aria-expanded`.

---

## 7. Known drift incidents (do not repeat)

The drift log lives in `console/locked-rules.md` rule 2.7 history. Short version of what has gone wrong before:

1. Public pages built with hand-rolled `<nav>` blocks instead of `PublicNav`. Wordmark drifted to LESARUSS PROJECT on /intake and /welcome.
2. PageHeader's eyebrow was orange (`var(--lr-orange)`) on white, failing AA at 10px (2.22 to 1).
3. Pages skipped the (public) route group, ended up without the fixed-nav padding, content sat under the nav.
4. Mocks loaded their own Google Fonts import despite the root layout already loading Montserrat. Inconsistent rendering across dev and prod.

Every one of those cost a round trip. The point of this skill is that the fifth entry never gets written.
