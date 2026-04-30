---
name: lesaruss-preflight
description: >
  LESARUSS brand preflight gate. USE THIS SKILL automatically every time Claude
  is about to share a link with the user. Triggers the moment Claude composes a
  markdown link [label](URL), a `computer://` link, or any "view your", "preview
  at", "live at", "deployed to", "here's the link", "open it at", "shared with
  you" phrasing that resolves to a URL share. Also fires when Claude renders a
  Sources: section. Do not wait for the user to ask. The point is to prevent
  off-brand artifacts from reaching Sean or any LESARUSS member under our name.
  Day 1 scope is the text brand baseline (no em-dashes, Vegan capital V,
  LESARUSS all-caps, Sean A. Russell spelling correct, GeekFon F-O-N, no
  Fieldy misspellings of LESARUSS). Auto-fix silently, re-run, share clean.
  Composes with `lesaruss-public-page` and `lesaruss-internal-page` (which
  catch issues at write time). This skill is the last gate before share.
  Canonical rule: console/locked-rules.md, rule 1.7.
---

# LESARUSS Brand Preflight, Last Gate Before Share

Run this every single time Claude is about to share a link with Sean or any
LESARUSS member. The skill is invisible when output is clean. The skill is
loud when output is off-brand. Either way, Sean only sees the final, clean
version.

The pattern is preflight, borrowed from aviation, adopted in print
publishing as Adobe PDF Preflight, and now adopted in AI marketing
compliance (puntt.ai, AuditSocials). Implementation borrows from Vale, the
prose linter Microsoft and Google use. The trigger surface ("Claude is
about to share a link") and the rule content are LESARUSS-original.

---

## 1. When this skill fires

Fires automatically the moment Claude is about to emit any of:

- A markdown link `[label](URL)` of any kind in chat
- A `computer://` link to a file in the workspace
- A `Sources:` section listing one or more URLs
- An inline phrasing that resolves to a URL share, including: "view your",
  "preview at", "live at", "deployed to", "deploy URL", "here's the link",
  "open it at", "shared with you", "the link is", "this is live at"
- Any Vercel deploy URL, Stripe checkout URL, or external service URL that
  Claude has just produced or referenced

When uncertain, fire. Running this skill is cheap. Sharing an off-brand
artifact is expensive.

---

## 2. The Day 1 rule set, text brand baseline

Each rule is a regex or a vocabulary check. All rules apply to the chat
text Claude is about to deliver, the link label inside that text, and the
artifact at the URL when it is a LESARUSS-controlled file Claude wrote in
the same turn. Rules do NOT apply to third-party page contents (we cannot
fix github.com or stripe.com), but they DO apply to anything Claude just
composed about that link.

**Rule A. No em-dashes anywhere.**

Pattern: U+2014 EM DASH (the glyph between the letter "e" and the word "dash" in this sentence: e dash dash dash). The skill matches the codepoint directly; this rule body deliberately avoids printing the glyph so the file stays clean.

Replacement: comma, period, colon, or plain hyphen, depending on context. The fix is contextual; it is not a blind find-and-replace.

| Em-dash usage (named, not shown) | Replace with |
| --- | --- |
| Mid-sentence aside (em-dash with spaces) | comma + space |
| Strong break (em-dash followed by capital) | period + capital letter |
| List intro (em-dash between item and description) | colon + space |
| Range (em-dash between two numbers) | the word "to" or a plain hyphen |

**Rule B. Vegan capital V, always.**

Pattern: `\b[Vv]egan(s|ism)?\b` where the first letter is lowercase.

Replacement: capitalize V. Applies to "vegan", "vegans", "veganism" in any
position in a sentence (mid-sentence and post-comma included). Brand-line
exception: there is none. Locked 2026-04-27.

**Rule C. LESARUSS spelled all caps, no Fieldy misspellings.**

Patterns to flag and replace with `LESARUSS`:
- `Lasaris`, `Lasarus`, `Lisarus`, `Osaris`, `Osiris` (case-insensitive)
- `Lesaruss`, `lesaruss` when not part of a URL or filesystem path
- `LESARUSS` written without all caps in body copy

The brand is L-E-S-A-R-U-S-S in caps in headlines and body copy. URLs
(lesaruss.ai, lesaruss.com) and filesystem paths (lesaruss-project,
lesaruss-context) keep their lowercase form by convention. Do NOT rewrite
URLs.

**Rule D. Sean A. Russell, spelled correctly.**

Patterns to flag and replace with `Sean A. Russell`:
- `Shawnee Russell` (voice transcription error)
- `Shawn Russell`, `Shaun Russell`, `Shon Russell`
- `Sean Russell` is acceptable in casual chat but flag if it appears in a
  shipped artifact (briefing, email, signed message) where the full name
  including middle initial is the locked form.

**Rule E. GeekFon, F-O-N, never GeekFun.**

Pattern: `GeekFun` (case-insensitive).

Replacement: `GeekFon`. The brand is fon, not fun.

---

## 3. Behavior

When the gate fires:

1. Scan the chat response Claude is about to deliver, plus any artifact at
   a LESARUSS-controlled URL Claude produced in the same turn. Apply rules
   A through E.
2. If any rule trips, auto-fix in place (text replacement) and re-run.
3. If after one pass the response is clean, share. Do NOT mention the
   check ran. Sean only sees the clean output.
4. If a rule trip is genuinely ambiguous (e.g., "vegan" is inside a quoted
   third-party headline that intentionally uses lowercase, or an em-dash
   is inside a code block representing actual user data), surface the
   single ambiguous case to Sean as an A/B option per rule 1.6 ("Keep as
   quoted, or normalize to LESARUSS spelling. A or B?"). One round trip
   on the genuine ambiguity is fine; round trips on auto-fixable nits are
   the bug this skill prevents.
5. Never share a link without running the gate.

The pattern is "check once, fix silently, deliver a one-line summary"
from rule 2.2 (ADA). This skill is the brand-text equivalent.

---

## 4. What this skill does NOT cover (yet)

Day 1 scope is text only. The following layers are deferred to later
amendments of rule 1.7 and will trigger their own prior-art checks:

- Visual baseline: locked color palette (#1A1A1A, #F69820, #555, #fff +
  per-brand accents), Montserrat font load, AAA contrast on every pair,
  white default canvas, no off-palette colors (the cream #fffaf0 panel
  that triggered this rule's creation would land here).
- Public-surface baseline: no BCPS or Title II references on public
  surfaces, no claim rail on LESARUSS-owned brands (rule 3.5), every
  page points to an action (universal).
- Email-specific baseline: Montserrat preferred with system fallback,
  white canvas, AAA on small text, plain-text body fallback for HTML
  email.

When these are added, they should each trigger `vetted-pattern-first` for
their own prior-art search before locking, even if the body of the rule
is short. The bar is "no rule lands without a prior-art check."

---

## 5. Composes with the existing template skills

- `lesaruss-public-page`, fires when a public-facing TSX or HTML page is
  being WRITTEN. Catches drift early, at the file level.
- `lesaruss-internal-page`, fires when an internal HTML page is being
  written. Same catch-early role.
- `lesaruss-preflight` (this skill), fires when a link is about to be
  SHARED. Last gate, regardless of whether the earlier skills fired or
  caught something.

The three are not redundant. Earlier skills catch most issues at write
time. This skill catches the rest at share time, when the user-visible
moment is about to happen. Defense in depth.

---

## 6. Provenance

- Pattern: brand preflight gate
- Closest public pattern: Adobe PDF Preflight (universal in print
  publishing); AI Pre-flight Checker category (puntt.ai, AuditSocials,
  getdevdone, 2025 to 2026)
- Implementation reference: Vale prose linter (rules-as-YAML data,
  Microsoft + Google adoption), Atlassian eslint-plugin-design-system
  (token enforcement), Lapidist design-lint (tokens-as-truth)
- LESARUSS recommendation: ADAPT
- LESARUSS-original parts: trigger surface (the LLM pre-share moment),
  rule content (Vegan-V, LESARUSS all-caps, Fieldy misspellings, Sean
  spelling, GeekFon)

Locked 2026-04-30 by Sean. Rule 1.7 in `console/locked-rules.md`.
