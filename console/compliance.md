# Compliance: Universal Rules

Locked 2026-04-21. Owner: Sentinel, Chief Compliance and Risk Console.

Any agent, station, or Cowork session operating on a LESARUSS surface reads this before publishing anything that will be seen outside the internal team. These three rules are not suggestions. They override older instructions anywhere they conflict.

---

## Rule 1: No humanized AI on public-facing surfaces

**What it means.** External audiences, members, clients, press, partners, the general public, must never be led to believe they are interacting with a human when they are interacting with AI. Human-style first names, headshot photos, and job titles that imply a person, are not allowed on public surfaces.

**Public-facing includes:**
- lesaruss.com and every brand domain
- lesaruss.ai (member app) at any route a logged-in member can reach
- Any PDF, slide, video, email, or social post that goes to someone outside LESARUSS
- The Huddle (members + clients), community chatbot, any PULSE tier 25 percent or higher

**Internal-only includes:**
- Mission Control, Daily Brief, Sean Report, agent meetings
- Cowork sessions with Sean or a LESARUSS-contracted operator
- Internal Supabase dashboards, internal playbooks, internal Slack / iMessage

**What to do instead.** Externally, refer to Consoles and Cartridges. "Sentinel, Chief Compliance and Risk Console." "Fieldy, the field capture Console." "The BCPS Cartridge." The product name does the work; the AI nature is transparent.

**Why this rule exists.** Anthropic's usage policy prohibits deceiving people about whether they are interacting with AI. California SB 1001 requires bot disclosure in consumer-facing interactions. California SB 942 imposes AI-transparency labeling. The EU AI Act adds interaction disclosure. The FTC treats AI-as-human as a deceptive practice. Beyond the law, this is a values decision: LESARUSS is on the B Corp track. Honesty about what the user is talking to is non-negotiable.

---

## Rule 2: Consoles and Cartridges are the external vocabulary

**What it means.** When describing how LESARUSS works to anyone outside the internal team, use "Console" (the product shell, the AI-powered specialist capability) and "Cartridge" (the brand or domain specialization loaded into a Console). Do not use internal team nicknames, persona names, or "agent" / "employee" / "GM" on external surfaces unless the target audience is already inside the internal team.

**Blueprint + Playbook stay internal.** Those words describe the why and the how of a system for the team. They are not product names.

**External copy pattern:**
- Instead of: "Sable built the login."
- Write: "The Infrastructure Console built the login."
- Instead of: "Marcus Webb owns sponsorship."
- Write: "The Partnerships Console, running the Sponsorship Cartridge, owns that lane."

**Where the roster still appears.** Internally, in Cowork, in the Directory app, in Mission Control, in team meetings. A member of the public does not see a roster of named AI people and does not need to.

**Why this rule exists.** It aligns the public story with what is actually being sold: a platform of Consoles that load Cartridges. Naming the product, rather than the persona, also removes the impersonation risk that Rule 1 blocks. It also keeps marketing consistent as the internal team composition shifts.

---

## Rule 3: Compliance Radar is mandatory before anything goes public

**What it means.** Any asset that will be seen outside the internal team runs through the Compliance Radar before publish. Radar checks seven categories: AI disclosure, data privacy, accessibility, copyright and licensing, FTC honesty, client confidentiality, and sector-specific rules. A Radar PASS is required before the asset moves from staging to production. A NEEDS HUMAN outcome routes to Sentinel for judgment. A FAIL blocks the publish until corrected.

**Scope.**
- Every new web page, email, video, slide, PDF, audio release, social post
- Every change to a public-facing copy block
- Every new client deliverable that will be sent outside LESARUSS
- Every module release that exposes a new user-facing surface

**Where the Radar lives.** `/playbooks/compliance-radar.html` in the LESARUSS HQ workspace. Sentinel owns the file and the routing rules.

**Where incidents are logged.** `/playbooks/compliance-incident-log.html`. Every catch, every miss, every near-miss. Patterns trigger protocol review.

**Where vendor rules are kept.** `/playbooks/tos-library.html`. The Radar reads from this library when scoring a submission.

**Why this rule exists.** The Huddle incident of 2026-04-21 established that a well-intentioned asset can carry multiple compliance risks, invisible until someone looks. Radar forces the look. One cost is a few minutes on each publish. The cost of skipping Radar is a lawsuit, a takedown, a retraction, or a breach of contract. Not a trade LESARUSS makes.

---

## Where these rules sit in the stack

- This file (`console/compliance.md`) is the universal rulebook. It is fetched at the start of every session by every agent with internet access to the Signal.
- `console/core.md` covers operating basics. This file extends it.
- `console/terminology.md` defines the product vocabulary. This file enforces external usage.
- `cartridges/brands/*.md` may add brand-specific compliance notes (FERPA for K12 Unlocked and BCPS, ADA obligations at the contractual level for ADA Unlocked). Those notes add to, never subtract from, this file.

## If these rules conflict with an older instruction

The older instruction is retired. This file wins until Sentinel and Sean update it together.

## Change log

- 2026-04-21, v1.0. File created. Triggered by the Huddle pre-publish catch.
