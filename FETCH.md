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

## Cartridge (load based on project)
- LESARUSS Platform: https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/cartridges/brands/lesaruss-project.md
- BCPS (K12 Unlocked): https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/cartridges/brands/bcps.md

Use WebFetch to retrieve each URL at conversation start. Apply all standards, terminology corrections, and team context from these files throughout the session.
```

---

## Notes

- Edits to this repo propagate to all connected workspaces within ~30 seconds (GitHub raw CDN cache)
- Console files are universal (load in every project)
- Cartridge files are project-specific (load only what applies)
- For client accounts: console + public industry cartridge (DIY), + starter client cartridge (Guided), + full custom cartridge (Structured/Done For You)
