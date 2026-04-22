# How to Connect a Claude Workspace

Paste the following into your Claude Project Instructions to auto-load LESARUSS context at session start.

---

## Instructions Block (copy everything below into Project Instructions)

```
# LESARUSS Context (auto-fetched)

At the start of every conversation, fetch and read the following files from the LESARUSS context repository. These contain the living operating context for the LESARUSS universe.

## Console (always load)
1. https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/console/core.md
2. https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/console/team.md
3. https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/console/standards.md
4. https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/console/terminology.md
5. https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/console/deploy.md
6. https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/console/compliance.md

## Cartridge (load based on project)
Pick the cartridge(s) that match the project. Full catalog below.

Use WebFetch to retrieve each URL at conversation start. Apply all standards, terminology corrections, and team context from these files throughout the session.
```

---

## Cartridge Catalog

Base URL for all cartridges: `https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/cartridges/brands/`

### Platform & Infrastructure
- `lesaruss-project.md` — LESARUSS platform (lesaruss.ai). Next.js 16, Supabase, Vercel. Load for any platform work.
- `lesaruss-360.md` — 360.lesaruss.ai. Modular personal OS app. Health is first module. Trainer-shareable profiles.
- `lesaruss-academy.md` — academy.lesaruss.ai. Training + Creative Producer certification. Paid product. Guaranteed employment for graduates.

### Sean A. Russell (personal brand cluster)
- `sean-a-russell.md` — seanarussell.com. Founder brand, anchor of the universe. Public reveal July 1, 2026.
- `from-blur-to-blueprint.md` — FBTB. Closed origin story. Lives on seanarussell.com.
- `blueprint-to-beyond.md` — B2B. Ongoing daily living series. Nia writes, Victoria reviews, Sean off the approval chain.
- `mogul-in-the-making.md` — Mockumentary reality series. $25K/trip floor. Ep 1 by June 1, 2026. Line Producer Console master.
- `the-blueprint.md` — Scripted animated sitcom. GeekFon Society setting. Franchise Bible v2.

### K12 Unlocked universe
- `k12-unlocked.md` — Umbrella brand. District-tech vertical. Finalsite rival. Brandon Cole owns.
- `bcps.md` — Broward County Public Schools client. Title II Apr 24, 2026.
- `chester-is-cool.md` — Animated family brand, K12 Unlocked client. Wren Calloway owns.
- `russells-roving-reporters.md` — Student journalism brand, K12 Unlocked client.

### Community & vertical brands
- `vegans-explore.md` — Flagship community brand. First live tenant on the platform.
- `ada-unlocked.md` — Universal accessibility layer. Imara Voss owns. Dev Okafor is CAO universe-wide.
- `111-day-theory.md` — Personal transformation framework. Dayo Adewale owns.
- `topspot.md` — Legacy brand, archive/showcase only.
- `anime3000.md` — Anime production studio + community. Pivoting from commentary.
- `geekfon-society.md` — Music + radio + podcast network. GeekFon Radio. Captivate pipeline queued.

### Music brands
- `shamanic-resin.md` — K-pop, anime-linked (Anime3000). Never conflate with Mad Tings.
- `mad-tings.md` — UK Grime, Dubstep, Reggae. Never conflate with Shamanic Resin. In-show premise of The Blueprint Ep 1.

---

## Notes

- Edits to this repo propagate to all connected workspaces within ~30 seconds (GitHub raw CDN cache)
- Console files are universal (load in every project)
- Cartridge files are project-specific (load only what applies)
- For client accounts: console + public industry cartridge (DIY), + starter client cartridge (Guided), + full custom cartridge (Structured/Done For You)
