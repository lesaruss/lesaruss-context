# ADA Unlocked Cartridge

## What This Is
ADA Unlocked is the LESARUSS accessibility product. A module, a service, and a standalone brand. Sold into every K12 Unlocked district deal. Overlays every LESARUSS tenant. Serves as a live case study of what universal WCAG 2 AA compliance looks like when built into the stack, not bolted on. Waiting room live on April 20, 2026 soft launch.

## Domain
- Primary URL: `adaunlocked.com`
- Runs as a module overlay on top of the LESARUSS platform, also sells as standalone

## Key People
- **Imara Voss** — General Manager, ADA Unlocked. Briefings Tuesday + Friday 10 AM.
- **Dev Okafor** — Chief Accessibility Officer (universe-wide, not ADA Unlocked GM). Reports to Victoria. Oversees compliance across every LESARUSS brand, handles compliance languaging.
- **Brandon Cole** — K12 Unlocked GM, co-sells ADA Unlocked with every district deal

## The Product
Three tiers (per `project_lesaruss_model.md`):
- $11 one-time (entry audit)
- $100/month (ongoing monitoring + remediation queue)
- $1,000/month (full remediation service + agent handoff)

Pipeline: automated `ada-checker` skill runs on every HTML/TSX/JSX/CSS change. Failures flagged to Imara's queue. Critical issues escalate to Dev Okafor. Remediation ships back to the tenant with a compliance stamp.

Vegans Explore is the first rollout tenant. K12 Unlocked districts are the first paid deals. BCPS Title II deadline Thu Apr 24, 2026 is the first hard case study.

## Overlap With Other Brands
- **LESARUSS Project (platform)** — ADA Unlocked is the compliance layer every tenant loads. Standards in `console/standards.md` are enforced by this product.
- **K12 Unlocked** — bundled into every district deal. Title II compliance is the wedge.
- **Vegans Explore** — first live overlay, case study lives in VE member experience.
- **Chester Is Cool + Russell's Roving Reporters** — kids and student content carries the strictest access requirements (captions, audio descriptions, reduced motion).
- **Mogul in the Making** — on-camera captions, transcripts, descriptive audio required for every episode.
- **LESARUSS Academy** — accessibility training courses live inside Academy, certification track for district teams.

## Rules
- WCAG 2 AA is the floor, not the ceiling. ADA Unlocked tenants target AAA where feasible.
- Orange `#F69820` fails on white at 2.22:1, never use as text on light backgrounds, reserve for large headings or focus rings
- `ada-checker` skill runs silently before any visual deliverable ships, per Sean's standing rule
- Every failure gets logged to the ADA Incident Log (`ada_incident_log.md`), never skipped
- Dev Okafor signs off on universe-wide compliance language, Imara signs off on ADA Unlocked product copy
- No em-dashes, ever

## How to Apply
When any agent works on accessibility, compliance audits, remediation, or district Title II deals, load this cartridge. For platform mechanics, also load `cartridges/brands/lesaruss-project.md`. For district rollouts, also load `cartridges/brands/k12-unlocked.md`.
