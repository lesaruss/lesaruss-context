# Vegans Explore Cartridge

## What This Is
Vegans Explore is the flagship community brand inside the LESARUSS Universe and the first live tenant on the multi-tenant platform. A vegan directory, community, and content layer that proves the LESARUSS stack on a real audience before every other brand deploys. Fully live on April 20, 2026 soft launch.

## Domain
- Primary URL: `veganseexplore.com` (root brand) and `vegansexplore.lesaruss.ai` (platform tenant)
- Stack: Next.js 16, Supabase, Stripe, Vercel (shared LESARUSS platform)
- Tenant ID: `vegansexplore` (see `project_entry_engine.md` memory for migrations)

## Key People
- **Victoria Egan** (President) covers brand direction until dedicated GM assigned
- **Sean A. Russell** (Founder, Chairman) closely involved, vegan since 2013, personal brand tie
- **Rami Okonkwo** (GM) operational
- **Nia Redmond** (Writer) content
- **Marcus Webb** (Partnerships) sponsorship + partner campaigns
- Agent roster: standard LESARUSS team scaled to VE tenant per `project_agent_team_scaling.md`

## The Product
Community platform with 5 builder types, assessment quiz, Stripe entry, monthly + annual + free + advanced tiers, directory, points economy, events.

Builder types (Vegans Explore):
- `pre_vegan` — The Curious Explorer
- `seasoned_vegan` — The Seasoned Vegan
- `entrepreneur` — The Vegan Entrepreneur
- `nonprofit` — The Nonprofit Builder
- `content_creator` — The Content Creator

Products per builder type: Toolkit, Cookbook, Blueprint (staggered release Jun 1, Jun 15, Jul 1). See `lib/entry-engine-config.ts`.

## Live Campaigns
- **Animal Hero Kids** — partner campaign. Brief at `playbooks/animal-hero-kids-campaign-plan.html`. Marcus Webb owns. Susan is partner contact.
- **Europe Outreach** — Sean's speaking tour July 2026. Valentina owns. VE enrollment moment in every talk.

## Overlap With Other Brands
- **Chester Is Cool** — family-facing health and education crossover. Chester introduces plant-based living to kids, VE holds the adult community. Partner campaigns should bridge both.
- **111 Day Theory** — personal transformation framework. Plant-based journey is a natural 111 cohort. VE members graduate into Theory cohorts for deeper personal work.
- **Mogul in the Making** — VE cities are tour stops. Each trip activates local VE chapters, captures member stories on camera, drives signups at events.
- **Sean A. Russell** — Sean's personal brand. Founder story is the hero narrative. SAR press hits drive VE signups.
- **ADA Unlocked** — VE is the first LESARUSS tenant to roll out ADA module. Serves as live case study.
- **GeekFon Society** — VE gets its own podcast show in the GeekFon Radio network when Captivate integration lands.

## Rules
- Never dark mode, LESARUSS orange `#F69820` and white are the anchors
- Always "Vegans Explore" (never "Vegan Explore," "VeganExplore," or "VE" in member-facing copy; "VE" acceptable internal shorthand only)
- All ADA/WCAG 2 AA standards from `console/standards.md` apply
- Paid content ships members-first per `console/compliance.md` Rule 4 (7-14 day member window, then public)
- Assessment quiz scoring is locked, do not redesign without CSO sign-off
- Free tier members are restricted from voting, favoriting, boosting, points economy (enforced at API layer)

## How to Apply
When any agent touches VE product, content, or partnerships, reference this cartridge. For platform mechanics (entry engine, directory, points, membership tiers) also load `cartridges/brands/lesaruss-project.md` since VE runs on that stack.
