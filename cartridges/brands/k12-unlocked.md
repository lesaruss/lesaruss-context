# K12 Unlocked Cartridge

## What This Is
K12 Unlocked is the umbrella brand for LESARUSS's education vertical. A platform and service layer for K-12 school districts, individual schools, and district-led media programs. Finalsite rival in the district-tech space. Waiting room live on April 20, 2026 soft launch.

## Domain
- Primary URL: `k12unlocked.com`
- Stack: Next.js 16, Supabase, Vercel (shared LESARUSS platform pattern)
- Sits under the LESARUSS Universe, shares auth and Console layer

## Key People
- **Brandon Cole** — General Manager, K12 Unlocked. Overall responsible for all clients under the umbrella.
- **Sean A. Russell** — Founder, Chairman. Former BCPS district webmaster. Domain credibility anchor.
- **Imara Voss** — GM, ADA Unlocked. Paired closely since K12 rollouts carry heavy ADA requirements.

## Clients Under The Umbrella
K12 Unlocked operates as umbrella, individual district/school brands operate as clients underneath it. Each client has its own cartridge.

- **BCPS** (Broward County Public Schools) — see `cartridges/brands/bcps.md`
- **Chester Is Cool** — see `cartridges/brands/chester-is-cool.md`
- **Russell's Roving Reporters** — see `cartridges/brands/russells-roving-reporters.md`

## The Product
District-tech platform covering site hosting, board meeting minutes, parent/community portals, accessibility compliance, district communications, and student media programs. BCPS Minutes is the first live product module.

## Overlap With Other Brands
- **ADA Unlocked** — K12 rollouts require Title II compliance by April 2026. ADA Unlocked is the compliance layer sold into every district deal. Imara + Dev Okafor pair on every district.
- **Chester Is Cool + Russell's Roving Reporters** — K12 clients that also function as student media brands. Kids are the content creators, districts are the distribution.
- **Vegans Explore** — school nutrition and plant-based lunch programs are a natural cross-sell into districts.
- **BCPS** — live case study. Every deal pitch references BCPS Minutes and the Title II rollout.
- **LESARUSS Academy** — teacher training and professional development modules live inside Academy, sold as add-ons to district deals.

## Rules
- Always "Broward County Public Schools" or "BCPS," never "Baltimore"
- Always "Chester Is Cool," never just "Chester"
- Title II deadline Thu Apr 24, 2026 for BCPS is a hard date; Brandon Cole + Dino own the rollout
- All district-facing copy must pass ADA/WCAG 2 AA; rollouts require ADA Unlocked compliance layer enabled
- Never hardcode district branding, districts are tenants with their own color + logo config
- No em-dashes anywhere

## How to Apply
When any agent references a school district, minutes system, education tech, Title II compliance, or student media, load this cartridge plus the relevant client cartridge (BCPS, Chester, RRR). For platform mechanics, also load `cartridges/brands/lesaruss-project.md`.
