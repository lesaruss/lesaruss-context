# LESARUSS Locked Rules

**Owner:** Sean A. Russell
**Updated:** 2026-04-28
**Purpose:** Single, scannable index of every LOCKED universal rule. Any rule listed here applies on every station, every Cowork session, every project, every brand. If a rule appears here AND in auto-memory, this file wins.

> Why this file exists: auto-memory is per-device. Rules that must apply everywhere have to live in this repo so the auto-fetch chain pulls them on every session start. Without this file, V Station and other secondary stations operate with the public-facing rules only and miss the operating rules. That gap is what produced the 2026-04-27 Authority Engine MD writeup incident.

---

## How to read this file

Each rule has three lines. The rule itself, the **Why**, and the **How to apply**. If a station ever produces output that violates one of these rules, the rule was either not loaded or not followed. Either way, it is a station-parity bug, not a creative call.

Rules grouped by domain.

---

## 1. Output format

### 1.1 HTML-only internal docs (LOCKED 2026-04-09, reaffirmed 2026-04-24)

Every internal LESARUSS deliverable is an HTML file in the locked template. Never deliver a `.md` file as a final artifact. Markdown is allowed only as raw notes inside the auto-memory directory or as a working scratch in `/tmp`, never as a finished playbook, briefing, report, blueprint, daily brief, ops doc, or any member-facing or Sean-facing surface.

**Why:** Sean reads on a real browser. Markdown in chat is invisible after the conversation closes. HTML in the project shell is durable, viewable from Finder, and indexable by the directory.

**How to apply:** Before producing any deliverable, ask: is this a finished artifact or a working note? If finished, output is `.html` using `_templates/internal-page-LOCKED.html`. If a working note, `.md` is fine and stays in `/tmp` or auto-memory.

### 1.2 Auto-push internal docs live (LOCKED 2026-04-24)

Every playbook, briefing, report, or internal HTML doc created in the LESARUSS Project folder is pushed to `public/<same-path>/` on `main` in the SAME turn it is created. Live on creation. No review cycle for internal docs.

**Why:** Internal docs need to be reachable by every station and every agent the moment they exist. A doc that lives only on one disk is invisible to V Station, future stations, scheduled tasks, and the rest of the team.

**How to apply:** When you write `playbooks/foo.html` in the Project folder, push it to `public/playbooks/foo.html` on `main` in the same commit. This is separate from the mock-to-prod preview rule below, which applies to public-facing pages, not internal docs.

### 1.3 Mock-to-prod preview (LOCKED 2026-04-24)

Every non-trivial public-facing page change ships to `public/v<N>/index.html` on `main` first. Sean reviews on real Vercel infrastructure. Only after approval is it ported into the routed page.

**Why:** Local mocks lie. CSS, fonts, and JavaScript behave differently on Vercel than they do in a local browser. A static preview on the same infrastructure as production is the only way to catch the gap.

**How to apply:** For any change to a public page on `lesaruss.com`, `lesaruss.ai`, or any brand domain, save the new state to `public/v<N>/index.html`, push, send Sean the Vercel preview link. Wait for approval. Then port into the routed page in a second commit.

### 1.4 Mock before push (universal)

Always show a visual HTML mock for approval before pushing any code or deploying anything to a public surface.

**Why:** Cheaper to fix in a mock than in production. The team's reputation is built on zero blatant layout errors reaching Sean.

**How to apply:** Generate the mock, post the path or preview URL, wait for approval. Combine with rule 1.3 when the change is non-trivial.

### 1.5 Every page points to an action (LOCKED 2026-04-24)

Every page, public or internal, must clearly point the reader to a next action. No dead-end pages. List pages must have per-card calls to action.

**Why:** A page without a next action wastes the click that brought the reader there. Every surface in the LESARUSS universe is a step in a flywheel. Dead ends break the flywheel.

**How to apply:** Before publishing any page, identify the next action. If you cannot, the page is incomplete. List pages need per-card CTAs in addition to the top-level CTA.

### 1.6 Always share a viewable link + a clear next step (LOCKED 2026-04-27)

Every wrap-up message after a completed process (deploy, push, file write, mock build, anything Sean might want to look at) MUST contain a direct clickable link to the result and an explicit next step framed as a concrete option (A or B). Never end with "go check it" without a URL. Never end with "let me know" or "thoughts?" without options.

**Why:** Sean is running 8 brands. If he has to figure out what URL to open or what decision to make next, that is friction every turn. He has flagged this as recurring drift more than once. The rule applies to every Cowork chat output, not just to pages.

**How to apply:**
- Deploy result: live URL as a markdown link, plus "open it, then say X or Y."
- File creation: `computer://` link, plus "open it, reply with edits or approval."
- Mock pushed: mock URL, plus "review and approve or list changes."
- Multi-brand pattern work: link to ONE representative URL, plus a yes/no on rolling the pattern across the rest.
- Never ask open-ended "what do you think" without a concrete A/B option attached.
- Never list multiple completed surfaces without picking THE ONE Sean should open first.

---


### 1.7 Brand preflight before every shared link (LOCKED 2026-04-30)

Before Claude shares any link with the user, a brand preflight check runs against (a) the link label text, (b) the surrounding chat response Claude is about to deliver, and (c) the artifact at the URL when it is a LESARUSS-controlled surface that Claude produced or modified in the same turn. Day 1 rule set is the text brand baseline:

1. No em-dashes anywhere. Replace with comma, period, colon, or plain hyphen.
2. Vegan, Vegans, and Veganism are always capital V.
3. LESARUSS is spelled L-E-S-A-R-U-S-S in all caps. Fieldy transcription misspellings (Lasaris, Lasarus, Lisarus, Osaris, Osiris) are always wrong.
4. Sean A. Russell is spelled correctly. Voice transcription often produces "Shawnee Russell"; that is always wrong.
5. GeekFon is spelled F-O-N, never GeekFun.

Behavior on fail: auto-fix silently, re-run the check, share clean. The check is invisible to Sean unless an issue is genuinely ambiguous, in which case Claude surfaces it as an A/B option per rule 1.6. Matches the existing "ADA check is silent, fix once, deliver a one-line summary" pattern from rule 2.2.

Visual baseline (palette, font, contrast, white default), public-surface baseline (no BCPS or Title II on public, no claim rail on owned brands), and email-specific baseline (Montserrat preferred with system fallback, AAA on small text) are intentionally OUT of Day 1 scope. They layer on as later additions to this rule, after the Day 1 baseline is stable.

**Why:** the 2026-04-30 activation-email incident. The Phase 2 magic-link email mock was shared without verifying that its panel color (#fffaf0 cream) was inside the locked palette. Sean had to flag it, costing one round trip. The pattern is preflight, well-known in aviation, print publishing (Adobe PDF Preflight), and now AI marketing compliance (puntt.ai, AuditSocials, getdevdone). Prior-art check via the `vetted-pattern-first` skill found Vale (rules-as-data prose linter, ~5k stars, Microsoft + Google adoption) and Atlassian's `eslint-plugin-design-system` as canonical implementation references. Recommendation: ADAPT. Adopt the name "preflight" and the rules-as-data architecture from Vale; keep the trigger ("the moment Claude is about to share a link") and the rule content LESARUSS-original.

**How to apply:** the `lesaruss-preflight` skill enforces this rule. It fires automatically the moment Claude composes a markdown link, a `computer://` link, or any phrasing that resolves to a URL share (view your, preview at, live at, here's the link, deployed to, Sources: section). Never hand-roll the check on every page. The skill is the single source of truth and inherits across every station via the standard skill-load chain.

---

## 2. Visual and accessibility

### 2.1 White-only universal default (LOCKED 2026-04-24, supersedes auto-theme)

Every surface across the LESARUSS universe defaults to white background with brand-appropriate ink. Dark mode is an opt-in module the user enables, never a default and never a time-of-day auto-switch.

**Why:** Brand consistency. Dark mode introduces too many ADA edge cases for a default. Sean's review cycle is faster on white. The dot-pulse animation reads cleanly on white only.

**How to apply:** Strip any auto-theme JavaScript from new pages. Default `data-theme` to `light` on every new template. The dark-mode module can opt the user in, but the universal default is white. Old pages still running the 6AM-6PM auto-theme block are stale and must be reset on next edit.

### 2.2 ADA WCAG 2 AA mandatory (universal, since launch)

Every visual output passes WCAG 2 AA before it reaches Sean. Run the check silently. Deliver a one-line summary. Never skip for speed or scope.

**Why:** ADA compliance is a brand commitment, not a suggestion. LESARUSS sells accessibility as a service. Failing internally would be malpractice.

**How to apply:** Run the `anthropic-skills:ada-checker` skill on any HTML, TSX, JSX, or CSS before showing it to Sean. See `console/standards.md` for color-contrast tables and the orange-on-white prohibition.

### 2.3 Internal page template locked (LOCKED 2026-04-15)

Every internal HTML page copies `_templates/internal-page-LOCKED.html`. Never hand-write the nav, drawer, footer, or CSS variables.

**Why:** Hand-written nav has caused four documented drift incidents. The template exists so the same correction never has to happen twice.

**How to apply:** Read `_templates/READ-ME-FIRST.md` first. Copy the locked template. Edit only inside `<main>` blocks marked `EDIT BELOW`. Use `_templates/relock.py <file>` to repair drifted pages.

### 2.4 Mock viewport switcher universal (LOCKED 2026-04-09)

Every HTML mock includes a desktop/tablet/mobile viewport switcher with an orange pull handle. Hamburger nav appears at tablet and mobile breakpoints. Drawer toggle stays visible at every breakpoint.

**Why:** Sean reviews on multiple devices. A mock without the switcher hides responsive bugs.

**How to apply:** Use the mock-shell partial bundled with the locked template. Do not omit the switcher even on small mocks.

### 2.5 Brand Profile template locked (LOCKED 2026-04-27)

The Brand Profile page (lesaruss.ai/c/<slug>) layout is locked. Eight sections in fixed order: hero, threshold, prototype, transformation, founder + brand structure, FAQ, universal CTA, footer. CSS variables, color tokens, status pill states, and section roles are fixed. The Founder card is universal across every brand (Sean A. Russell). The FAQ is universal (six questions, copy locked in `lib/campaigns.ts` UNIVERSAL_FAQ). The Brand Structure card is per-brand with exactly three role types.

**Why:** Visual consistency across all eight brands. Per-brand drift on a profile page costs trust and breaks the universe-as-one-system promise. The funding mechanic (continuous, no deadline, no escrow) only reads cleanly when the layout is identical from brand to brand.

**How to apply:**
- Canonical reference: `_templates/brand-profile-LOCKED.html` in this repo.
- Routed implementation: `components/CampaignProfile.tsx` in `lesaruss-project`.
- Data contract: `Campaign` interface in `lib/campaigns.ts`.
- To add a new brand profile: add to `BRANDS` in `lib/brands.ts`, add an overlay to `OVERLAYS` in `lib/campaigns.ts`. Do NOT modify the CampaignProfile component layout.
- Optional logo asset on the hero: set `heroAssetPath` in the overlay; otherwise the monogram + brand-color gradient fallback renders.
- Status states drive CTA copy: active = "Pledge & move the line", draft = "Notify me", launched = "Enter the brand", archived = "Read the case study".
- Pairs with rule 3.5 (no claim rail on LESARUSS-owned brands).
- Any layout change requires explicit Sean approval and an update to this rule plus the locked HTML template.

### 2.6 Mock font lock, Montserrat (LOCKED 2026-04-28)

Every LESARUSS HTML mock, preview, briefing, playbook, internal page, public-surface mock, and design exploration must load **Montserrat** from Google Fonts at the top of the file. Falling back to `system-ui` or `ui-sans-serif` alone is non-compliant. Production lesaruss-project public HTML uses Montserrat everywhere; mocks that skip the import predict a render production never produces.

**Canonical include block (paste verbatim into every mock head):**

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@200;300;400;500;700;800;900&display=swap" rel="stylesheet">
```

**Canonical body font stack:**

```css
font-family: "Montserrat", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
```

**Why:** Production uses Montserrat across `public/signal/`, `public/v3/` through `v5/`, `public/preview/`, `public/proof-tools/`, the brand SVG logo (`public/brand/lesaruss-logo-light.svg`), and `modules/geekfon-radio.js`. Brand voice (extrabold uppercase headings, extralight body) maps directly to Montserrat 800 and 200. When a mock loads only the system stack, every operating system substitutes a different family and the mock fails to predict what production will render. Sean flagged this drift on 2026-04-28: "the font is still not locking in on these mocks. What fix was put in and why isn't it remembering the settings?" Truth: nothing was locked, no rule existed, no skill enforced it. This rule is the lock.

**How to apply:**

- Every new HTML mock starts by pasting the include block above into the head, before the `<style>` block.
- The body `font-family` is the canonical stack above. Every other selector uses `font-family: inherit`.
- `_templates/internal-page-LOCKED.html` already pre-includes Montserrat. Verify on every relock pass.
- The upcoming public-page locked template (rule TBD, route group `(public)`) must pre-include this block.
- Email HTML at `lib/email.ts` currently uses Helvetica Neue. That is a separate fix and is not covered by this rule.
- This rule pairs with rule 2.2 (ADA WCAG 2 AA): font choice does not exempt mocks from the AA contrast and focus-ring requirements.

### 2.7 Public page template lock (LOCKED 2026-04-28)

Every route on a LESARUSS public surface (lesaruss.ai, project.lesaruss.com, brand subdomains) lives inside the `app/(public)/<route>/page.tsx` route group of the lesaruss-project repo. The route group's `app/(public)/layout.tsx` automatically wraps every public page in `PublicNav` + `PublicFooter`. Hero blocks use `components/public/PageHero.tsx` (display) or `components/public/PageHeroCompact.tsx` (form pages). Member shortcuts use `components/public/MemberBanner.tsx`. Hand-rolled `<nav>` and hand-rolled hero blocks are forbidden on public surfaces.

**Why:** Before the lock, the four public pages on the codebase (`/`, `/intake`, `/welcome`, `/entry`) each carried their own inline nav with a different wordmark treatment, and `components/PageHeader.tsx` rendered the eyebrow in `var(--lr-orange)` on white which fails WCAG 2 AA at 10px (2.22 to 1). Every public-page change had to fix the same nav/footer/hero drift twice. The lock removes the drift surface.

**How to apply:**
- New public route: create `app/(public)/<route>/page.tsx`. Do NOT import or render `PublicNav`/`PublicFooter` inside the page body, the route-group layout already does that.
- Hero block: use `<PageHero>` (display) or `<PageHeroCompact>` (forms). Eyebrow color is `var(--lr-text-50)` (#555 on white = 7.5 to 1), never orange.
- Wordmark on every public page is `LESARUSS.AI` with the dot pulse. Legacy `LESARUSS PROJECT` is retired.
- Font is Montserrat from the root layout, weights 200, 300, 400, 500, 700, 800, 900 per rule 2.6. Do NOT add a Google Fonts link tag inside a public page.
- Mock-to-prod preview per rule 1.3: ship `public/v<N>/<route>/index.html` first, review on real Vercel infra, then promote into the routed page.
- ADA pass per rule 2.2 is mandatory. The locked hero family already passes; custom additions need a re-run.
- Skill `lesaruss-public-page` mirrors `lesaruss-internal-page`. It triggers automatically whenever an agent creates or edits a public-surface file. Install it on every station per rule 5.2.

**Locked artifacts (lesaruss-project repo):**

| Artifact | Path |
|---|---|
| Route-group shell | `app/(public)/layout.tsx` |
| Top nav | `components/PublicNav.tsx` |
| Footer | `components/PublicFooter.tsx` |
| Display hero | `components/public/PageHero.tsx` |
| Form hero | `components/public/PageHeroCompact.tsx` |
| Member banner | `components/public/MemberBanner.tsx` |
| Reference page | `app/(public)/intake/page.tsx` |
| v1 preview | `public/v1/intake/index.html` |


---

## 3. Voice and content

### 3.1 No em-dashes (universal, ever)

Never use em-dashes anywhere. Not in writing, not in code, not in comments, not in copy. Use a comma, period, colon, or plain hyphen.

**Why:** Sean's stylistic preference. Strong enough that it counts as a brand rule.

**How to apply:** Search and replace any em-dash before delivery. Auto-correct your own output as you write.

### 3.2 LESARUSS spelling (universal)

The brand is always spelled LESARUSS, all caps. Common Fieldy transcription misspellings are always wrong: Lasaris, Lasarus, Lisarus, Losarus, Osaris, Osiris, Licelra, Lazzara. Correct silently before using any content.

**Why:** Voice transcription garbles the brand name. Publishing the garble is a credibility hit.

**How to apply:** See `console/terminology.md` for the full correction table. Apply the table to every voice transcript before any other processing.

### 3.3 Members-first content (LOCKED 2026-04-21)

Every LESARUSS content asset ships to paying members on `lesaruss.ai` first, with a 7 to 14 day window before public release. Universal across every brand and every content type.

**Why:** Members pay for early access. The window also acts as a quality gate.

**How to apply:** When drafting any publish plan, default to members first. If someone proposes public first, flag it and ask why. See `console/compliance.md` Rule 4 for full scope.

### 3.4 No agent personas on forward-facing surfaces (LOCKED 2026-04-21)

Persona names live in the internal team only. External surfaces refer to Consoles and Cartridges, never to "Sable" or "Marcus Webb" or "Sentinel" as if they were people.

**Why:** Anthropic policy, California SB 1001, EU AI Act, FTC. Plus values: honesty about what the user is talking to.

**How to apply:** External copy says "the Infrastructure Console built the login," not "Sable built the login." Internal Cowork sessions can use persona names freely.

### 3.5 No claim rail on LESARUSS-owned brands (LOCKED 2026-04-26)

Strip the "Is this your brand?" section from every LESARUSS-owned profile. Claim rails appear only on third-party directory listings.

**Why:** The brand is already owned by LESARUSS. A claim rail invites confusion and potential bad-faith claim attempts.

**How to apply:** When generating brand pages for LESARUSS-owned brands (Vegans Explore, Chester Is Cool, K12 Unlocked, etc.), do not include the claim section. For directory listings of third-party brands, the claim rail stays.

---

## 4. Deploy

### 4.1 Vercel commit author must be Sean A. Russell (LOCKED 2026-04-25)

Every commit pushed to a Vercel-deployed repo (`lesaruss-ai`, `lesaruss-project`, brand repos) is authored as `Sean A. Russell <contact@lesaruss.com>`. Never `claude@lesaruss.ai` or any other identity.

**Why:** A commit authored by `claude@lesaruss.ai` triggers an instant Vercel ERROR with empty build logs because `githubCommitAuthorLogin` is missing from the deploy meta.

**How to apply:** Set `git config user.name "Sean A. Russell"` and `git config user.email "contact@lesaruss.com"` on every clone before commit. When using the GitHub Contents API, pass `committer.name = "Sean A. Russell"` and `committer.email = "contact@lesaruss.com"`.

### 4.2 Push via GitHub API or sandbox git, never an unaided terminal

Pushes happen one of two ways: Chrome MCP plus GitHub Contents API for chunked or multi-file uploads, or a sandbox `git clone` plus `git push` for fast multi-file batches. Do not ask Sean to paste git commands into an interactive terminal.

**Why:** Sandbox proxy blocks `api.github.com` (403) but allows `github.com` HTTPS (200). Both supported paths work. Asking Sean to type git commands violates the minimal-involvement preference.

**How to apply:** See `console/deploy.md` for both code paths. Use sandbox git push by default. Fall back to Chrome MCP if the file is over 6KB and base64 chunking is needed.

### 4.3 No terminal commands without copy-ready blocks

When a terminal step is unavoidable, give the full command in a single copy-ready code block.

**Why:** Sean copies once and pastes. Multiple commands across paragraphs cost time.

**How to apply:** One block per command sequence. No prose between commands inside a block.

### 4.4 Deploy from the actual repo, not the working folder (LOCKED 2026-04-27)

`lesaruss.ai` is served by the **lesaruss-project** Vercel project (Next.js framework), GitHub repo `lesaruss/lesaruss-project`, deployed files at `public/{path}.html`. Static HTML at `public/playbooks/{slug}.html` is served as `/playbooks/{slug}.html`. The lesaruss-ai repo (static) serves `hq.lesaruss.ai` only, with files at the repo root. Always identify the correct repo before pushing, and always push via a fresh `/tmp/` git clone, never by trusting a Google-Drive working folder to mirror the deployed branch.

**Why:** The HQ Google Drive folder at `/LESARUSS HQ--Claude--Projects--LESARUSS Project/` is a working tree of the lesaruss-project repo, but is OUT OF SYNC with the deployed branch. It has duplicate `playbooks/` directories at top level (legacy) AND at `public/playbooks/`. Only the `public/playbooks/` content actually deploys. Tier 1 + Tier 2 Playbook stubs live in `public/playbooks/`, NOT at the HQ folder's top-level `playbooks/`. On 2026-04-27 second pass, an agent burned ten minutes pushing to the wrong repo (lesaruss-ai instead of lesaruss-project) because lesaruss.ai serves from lesaruss-project and the agent assumed the repo name matched the domain.

**Domain to repo to deploy path map (canonical):**

| Domain | Vercel project | GitHub repo | Framework | Static path |
|---|---|---|---|---|
| lesaruss.ai | lesaruss-project | lesaruss/lesaruss-project | Next.js | `public/{path}` |
| project.lesaruss.com | lesaruss-project | lesaruss/lesaruss-project | Next.js | `public/{path}` |
| directory.lesaruss.com | lesaruss-project | lesaruss/lesaruss-project | Next.js | `public/{path}` |
| vegansexplore.lesaruss.com | lesaruss-project | lesaruss/lesaruss-project | Next.js | `public/{path}` |
| hq.lesaruss.ai | lesaruss-ai | lesaruss/lesaruss-ai | static | repo root |

**How to apply:**
- Before any deploy, look up the domain in the table above. Pick the correct repo.
- Clone the repo into `/tmp/<short>` with `--depth 1`. Do not edit files in the Google Drive working folder and assume they will deploy.
- Edit files at the correct path (`public/{path}` for lesaruss-project, repo root for lesaruss-ai).
- Commit + push as Sean A. Russell per rule 4.1.
- Verify via Vercel MCP `list_deployments` and a `curl -sI` against the live URL.
- If you find the working folder out of sync with the repo, do not silently sync it back. Flag the drift to Sean.

### 4.5 Persistent deploy clones live at ~/Code/&lt;repo&gt; (LOCKED 2026-04-27)

Every station keeps a real `git clone` of every active deploy repo at `~/Code/<repo>` on the host filesystem. That clone is the working copy for daily edits, scheduled-task pushes, and long-running agent work. The `/tmp/<short>` clone pattern from rule 4.2 is reserved for one-off operations or when `~/Code/<repo>` is not yet provisioned on a fresh station. **Never edit files in a Google Drive working folder and assume they will deploy.** Drive is a journal, not a deploy source.

**Why:** Three copies of the same file (Drive, Documents working folder, GitHub) silently drift, force a reconciliation step on every push, and cost cycles fixing rather than shipping. The 2026-04-27 HQ-promotion push hit this directly, and the same-day audit found 66 logical-path overlaps between Drive and `lesaruss-project` with em-dash fixes that had been applied in Drive but never propagated to the deployed branch. Consolidating to one canonical source per repo eliminates the drift surface.

**Domain to clone path map (canonical):**

| Repo | Local clone path |
|---|---|
| lesaruss-ai | `~/Code/lesaruss-ai` |
| lesaruss-project | `~/Code/lesaruss-project` |
| lesaruss-context | `~/Code/lesaruss-context` |

**How to apply:**
- On any new station, run `mkdir -p ~/Code` once, then `git clone https://github.com/lesaruss/<repo>.git ~/Code/<repo>` for each active deploy repo.
- Inside each clone, set local identity: `git config user.name "Sean A. Russell"` and `git config user.email "contact@lesaruss.com"` per rule 4.1.
- For daily work, edit files in `~/Code/<repo>` directly. Commit + push from there. Vercel auto-deploys.
- For ephemeral agent ops where a fresh tree is preferable, use the `/tmp/<short>` clone pattern from rule 4.2.
- The Google Drive `LESARUSS Project/` folder is being phased out as a deploy source. Treat any HTML or JSON file there as suspect until rule 4.5 has landed on every active station.

---

## 5. Station parity

### 5.1 The repo is the single source of universal rules

Every rule that applies on every station lives in this repo. If a rule lives only in auto-memory, it is per-device by design and does not propagate.

**Why:** Auto-memory is the journal of one device. The repo is the brain of the universe.

**How to apply:** When a new universal rule is locked, add it to this file and push. Do not save it to auto-memory only and assume secondary stations will pick it up.

### 5.2 Plugin and skill parity across stations

Every LESARUSS station runs the same plugin and skill set: `lesaruss-internal-page`, `ada-checker`, `deploy-troubleshooter`, `lesaruss-agent-setup`, `productivity` plugins, `engineering` plugins, `anthropic-skills` plugins. Verified at the end of the New Station Quickstart Playbook, Phase F.

**Why:** A skill that fires automatically on Sean's main station does not fire on V Station if it is not installed there. The Authority Engine MD writeup incident on 2026-04-27 was caused by missing skills on V Station.

**How to apply:** Every new station completes Phase F of the New Station Quickstart Playbook. The acceptance check is a `list_skills` output that matches the canonical roster.

---

### 5.3 Memory routing protocol (LOCKED 2026-04-27)

When a new universal rule is locked, it MUST be written to this repo, not only to per-device auto-memory. Local auto-memory is for journal-style observations (project state, session handoffs, references). Universal rules belong in the repo where every station fetches them.

**Routing decision tree.** Before saving any new memory, ask three questions in order.

1. Does the memory describe a rule that applies on every station, every brand, every project? If yes, it is universal. Save it to `console/locked-rules.md` in this repo. Add a one-line pointer in local `MEMORY.md` that links to the repo file. Do not duplicate the body.
2. Does the memory describe state of one project, one brand, one client, one incident, one decision in flight? Save it to local auto-memory only. Do not push to the repo.
3. Is it a reference to an external system (Linear project, Slack channel, dashboard URL)? Save to local auto-memory as a reference type. Repo not involved.

**Why:** the 2026-04-27 V Station incident was caused by a LOCKED rule (auto-push playbooks) living in local memory only. V Station never saw it. The fix is not to push everything to the repo, it is to consistently route the universal rules to the repo and the per-device journal to local memory.

**How to apply:** every time a memory is being saved, run the routing decision tree above. If a memory is universal, the body lives here, the local index just points. When a rule changes from project-specific to universal (which happens), the rule's body migrates from local memory to this file in the same turn the upgrade is recognized.

---

## Change log

- 2026-04-27, v1.0. File created. Triggered by V Station producing an MD playbook with no awareness of the auto-push or HTML-only rules. Migrated 14 rules from per-device auto-memory into the repo so they apply on every station.
- 2026-04-27, v1.1. Added rule 1.6 (Always share a viewable link + a clear next step). Triggered by recurring chat-output drift where Cowork messages closed without a link or a concrete next step.
- 2026-04-27, v1.2. Added rule 5.3 Memory routing protocol so future LOCKED universal rules land here automatically instead of in per-device auto-memory.
- 2026-04-27, v1.3. Added rule 4.4 (Deploy from the actual repo, not the working folder) plus the domain-to-repo-to-path map. Triggered by 2026-04-27 second-pass push where an agent burned ten minutes cloning the wrong repo because lesaruss.ai (deployed from lesaruss-project) was assumed to deploy from lesaruss-ai.
- 2026-04-27, v1.4. Added rule 2.5 (Brand Profile template locked). Triggered by Sean lock-in after GeekFon Society profile shipped and the eight-brand rollout was about to begin. Pairs with new `_templates/brand-profile-LOCKED.html` artifact.
- 2026-04-27, v1.5. Added rule 4.5 (Persistent deploy clones live at `~/Code/<repo>`). Triggered by file architecture migration Phase 1, which surfaced 66 logical-path overlaps between Drive and `lesaruss-project` (including 20 em-dash fixes that had been applied in Drive but never propagated to the deployed branch). Pairs with the migration playbook at `hq.lesaruss.ai/playbooks/file-architecture-migration-playbook`.
- 2026-04-28, v1.6. Added rule 2.6 (Mock font lock, Montserrat). Triggered by Sean noticing that the intake v2 mock at `LESARUSS Project/mocks/intake-v2.html` declared a system stack only and rendered with the wrong family. He asked "what fix was put in and why isn't it remembering the settings?" Audit found no prior rule, no shared mock template, no skill enforcement. Production uses Montserrat across every public surface; mocks that skip the import drift on every render. Local memory pointer at `feedback_mock_font_lock.md` updated to canonical-in-repo status.
- 2026-04-28, v1.7. Added rule 2.7 (Public page template lock). Triggered by Sean lock-in after intake-v2 mock approval and audit found 4 different inline navs across `/`, `/intake`, `/welcome`, `/entry` plus a PageHeader eyebrow that fails AA on white. Pairs with new `app/(public)/` route group + `components/public/` hero family in lesaruss-project, and the new `lesaruss-public-page` skill mirroring `lesaruss-internal-page`.
- 2026-04-30, v1.8. Added rule 1.7 (Brand preflight before every shared link) plus skill `lesaruss-preflight`. Triggered by 2026-04-30 chat: the Phase 2 activation-email mock at `lesaruss.ai/v2/activation-email/index.html` was shared without verifying the cream panel color (#fffaf0) was inside the locked palette. Sean asked "make sure it's on brand" and "this should feed across all stations in the Universe." Prior-art search by `vetted-pattern-first`: ADAPT preflight (Adobe PDF Preflight, AI marketing compliance category) + Vale rules-as-data architecture (Microsoft + Google adoption). Day 1 scope is the text brand baseline only (em-dashes, Vegan-V, LESARUSS spelling, Sean spelling, GeekFon). Visual + public-surface + email baselines deferred per Sean's calibration so the rule lands clean before scope expands.
