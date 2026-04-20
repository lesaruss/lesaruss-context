# BCPS Cartridge — Broward County Public Schools

## What This Is
BCPS is a client under the K12 Unlocked brand. Brandon Cole is overall responsible. This cartridge gives any agent working in the BCPS project the context they need to operate without breaking things.

## Key People
- **Brandon Cole** - Overall responsible for BCPS (K12 Unlocked)
- **Alex** - Ops team
- **Dino** - Ops team
- **Brandon Graham** - Ops team
- **Sean Russell** - Chairman (NEVER write "Baltimore" for BCPS - it is Broward County, South Florida)

## The Product
**BCPS Minutes** - A board meeting minutes management app.
- Live at: `bcps.lesaruss.com`
- Repo: `lesaruss/bcps-minutes`
- Stack: Next.js, Vercel, Supabase
- Deploys automatically to Vercel on every push to main

## Critical Date
- **Title II deadline: Thu Apr 24, 2026** - Hard stop. Brandon Cole + Dino must act.

## The Signal — What It Is
The Signal is the central LESARUSS knowledge base. It is NOT a separate app or codebase.

- **What it is:** A public GitHub repo that agents fetch context from
- **Where it lives:** `lesaruss/lesaruss-context` (this repo)
- **How to use it:** Fetch raw files via `raw.githubusercontent.com` URLs
- **NOT:** A repo called `lesaruss/signal` — that does not exist

When someone says "push to The Signal," they mean: push a context/documentation file to `lesaruss/lesaruss-context`.

## PULSE — Communication Layer
PULSE is the tiered communication system built on top of The Signal. Do not confuse PULSE with a codebase. It is a product family.
- v1 (Sean only): iMessage to V Station + Fieldy voice memos - LIVE
- 25%/50%: Member chatbots - Planned
- 75%: The Huddle (web meeting room) - In design
- 100%: Own infrastructure - Future

## Deploy Rules (BCPS)
All code pushes go through Chrome MCP + GitHub Contents API. Never use the terminal for GitHub operations. See `console/deploy.md` for the full workflow.

Repo: `lesaruss/bcps-minutes`
PAT: stored in auto-memory at `reference_github_pat.md`

## Naming Rules
- Always: **LESARUSS** (all caps, L-E-S-A-R-U-S-S)
- Always: **Broward County** (never Baltimore)
- Always: **The Signal** (never Cerebro - that name is retired)
- Always: **GeekFon** (F-O-N, not GeekFun)
- Never use em-dashes. Use commas, periods, colons, or plain hyphens.
