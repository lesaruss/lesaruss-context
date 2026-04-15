# LESARUSS Internal Page Template — Pre-Flight Checklist

**Locked 2026-04-15 by Sean.** If you are about to create or edit an internal LESARUSS HTML page (playbook, briefing, report, blueprint, mock, daily brief, ops doc, agenda, meeting notes, any member-facing internal page), you MUST read this file first.

## Mandatory pre-flight

1. Open `_templates/internal-page-LOCKED.html` with the Read tool.
2. Copy that file to your destination. Do not hand-write the nav, drawer, footer, or CSS variables.
3. Only edit content inside the `<main>` block marked `EDIT BELOW`.
4. Swap the three module icons in `.nav-right` for the modules the current user has loaded. Keep the SR avatar.
5. If you find a reason to deviate from the locked template, STOP and ask Sean before continuing.

## What is locked

- Top bar: LESARUSS.AI wordmark with pulsing dot (left). Module icons as 32px circles + SR avatar (right). No horizontal nav links.
- Module icons: 32x32, border-radius 50%, `--lr-surface2` bg, `--lr-border` border, 14px SVG at `--lr-text-50`, hover to `--lr-orange-text`.
- Left-edge drawer toggle: 26x64 orange rectangle, default closed, periodic subtle pulse every ~12s.
- Left drawer: Mission Control, Brand, Directory, Library, Playbooks, Modules, Settings. Closes on scrim, X, or Escape.
- Font: Montserrat via Google Fonts, weights 400/600/700/800/900.
- CSS variables: `--lr-*` prefix. Light mode orange-text is `#7d4a00` for ADA.
- Auto theme: light 6AM to 6PM local, dark 6PM to 6AM. No manual toggle.
- Footer: LESARUSS.AI mark + footer nav + copyright.
- Page wrap: `<main>` max-width 1100px, padding `110px 28px 80px`.

## Known drift incidents (do not repeat)

| Date | What drifted | Why |
|---|---|---|
| 2026-04-15 | Used console-cartridge-playbook nav (top-right avatar, no left drawer) | Referenced wrong canonical file. |
| 2026-04-15 | Used HQ-seeding-checklist nav (dark outer bg, white frame, viewport switcher only) | Referenced older template. |
| 2026-04-15 | Rebuilt from live /brand page but kept horizontal nav links in top bar | Sean wants primary nav in a left drawer, not the top bar. |
| 2026-04-15 | Used square icons instead of 32px circles | Missed the module-registry canonical icon pattern. |

Each incident cost a round trip with Sean. The locked template exists so the same correction never has to happen twice.

## Canonical references

- Template file: `/Documents--Claude--Projects--LESARUSS Project/_templates/internal-page-LOCKED.html`
- Reference playbook built from the template: `/Documents--Claude--Projects--LESARUSS Project/playbooks/resume-building-module-playbook.html`
- Memory spec: `/.auto-memory/feedback_internal_nav_standard.md`
- Module icon source-of-truth: `/LESARUSS HQ--Claude--Projects--LESARUSS Project/playbooks/module-registry.html` (section `.nav-module-icon`)

## When in doubt

Diff your page against the locked template. If the nav, drawer, footer, CSS variables, or icons differ, you are wrong. Reset and copy the template.
