---
name: lesaruss-session-preflight
description: >
  LESARUSS session preflight gate. USE THIS SKILL automatically before the
  first tool call of any conversation that is going to do real work: editing
  files, deploying, pushing, generating a mock, writing a briefing or
  playbook, touching a member-facing surface, or executing a "Continue"
  command. Triggers on the first sign of substantive work, not on pure
  conversation turns. The job is to verify that the canonical universal
  rules are loaded into working memory before any irreversible action runs.
  Day 1 scope is fetch-verification only, did core.md and locked-rules.md
  get pulled this session. Composes with lesaruss-preflight (per-link gate)
  and lesaruss-internal-page / lesaruss-public-page (write-time gates).
  This skill is the per-session gate. Silent on pass, loud on partial or
  fail, postscript on skip.
  Canonical rule: console/locked-rules.md, rule 1.8.
---

# LESARUSS Session Preflight, Gate Before First Tool Call

Run this once per conversation, before the first tool call that does real
work. The skill is invisible when output is clean. The skill is loud when
context is missing. Either way, Sean only sees the final, clean session.

The pattern is preflight, borrowed from aviation, adopted in print
publishing as Adobe PDF Preflight, and now mainstream in agentic AI
(see "Agent Safety Gates: 12 Preflight Checks Before Tools Run", Medium,
March 2026; "Preflight the Plane", AI-Assisted Software Development).
Implementation borrows the index-first progressive-disclosure pattern
documented at MindStudio. The trigger surface ("first substantive tool
call of a session") and the rule content are LESARUSS-specific.

This skill is the SISTER of `lesaruss-preflight`. That one fires per
shared link. This one fires per session. Both are silent on pass.

---

## 1. When this skill fires

Fires automatically the moment Claude is about to take any of these
actions for the first time in a conversation:

- Any file write or edit (Write, Edit, NotebookEdit, file_upload)
- Any git push, GitHub API commit, Vercel deploy, or Supabase migration
- Any HTML mock, briefing, playbook, report, or design artifact creation
- Any modification of a member-facing surface (lesaruss.ai, brand pages,
  intake, welcome, entry, signal, mission control, directory)
- Any "Continue" command from Sean
- Any scheduled-task creation or update
- Any agent profile creation or persona change

Does NOT fire on:

- Pure conversation turns (questions, explanations, planning discussions)
- ToolSearch calls used to load deferred tools
- WebFetch or WebSearch used for prior-art / research only
- Reads of canonical context files (this skill's own work)

When uncertain, fire. Running this skill is cheap. Operating with stale
or missing universal rules is expensive — it is exactly what produced the
2026-04-27 V Station MD writeup incident and the recurring drift Sean
flagged in the 2026-05-05 "why does this keep happening" conversation.

---

## 2. The Day 1 check, fetch verification

The single check on Day 1 is: have the canonical context files been
fetched into working memory this session?

The canonical fetch list (from project instructions, mirrored here):

1. `console/core.md`
2. `console/team.md`
3. `console/standards.md`
4. `console/terminology.md`
5. `console/deploy.md`
6. `console/compliance.md`
7. `console/locked-rules.md`
8. The brand cartridge for the active project (e.g.,
   `cartridges/brands/lesaruss-project.md`)

If any file in this list has not been fetched this session, the skill
fetches it now via WebFetch against
`https://raw.githubusercontent.com/lesaruss/lesaruss-context/main/<path>`.

After fetch completes, the skill confirms the top universal rules are
present in working memory by name. Day 1 confirmation list:

- Rule 1.1 HTML-only internal docs
- Rule 1.2 Auto-push internal docs live
- Rule 1.3 Mock-to-prod preview
- Rule 1.4 Mock before push
- Rule 1.5 Every page points to an action
- Rule 1.6 Always share a link + clear next step
- Rule 1.7 Brand preflight before every shared link
- Rule 2.1 White-only universal default
- Rule 2.2 ADA WCAG 2 AA mandatory
- Rule 3.1 No em-dashes
- Rule 3.2 LESARUSS spelling
- Rule 4.1 Vercel commit author = Sean A. Russell
- Rule 5.3 Memory routing protocol

This list is a confirmation marker, not the rule body. Bodies live in
`console/locked-rules.md` and are pulled into context by the fetch step
above.

---

## 3. Output behavior

**On PASS (all canonical files loaded, all rules confirmed):** silent.
No chat output. Proceed to the originally-requested tool call. The user
should never see a passing preflight, only its absence of consequences.

**On PARTIAL (some files loaded, some missing):** print one line:

```
Preflight: PARTIAL — fetched [N missing files], proceeding.
```

The fetch happens automatically, no Sean intervention required. The line
exists so the next chat-length audit can spot any session that started
with stale context.

**On FAIL (canonical fetch failed, network / repo unreachable):** print:

```
Preflight: FAIL — could not reach lesaruss-context repo. Proceeding with
last-known canonical rules from auto-memory. Flag any drift immediately.
```

Then proceed with degraded confidence. Do not block Sean's request on a
network hiccup. Do flag the failure clearly so subsequent output gets
extra scrutiny.

**On SKIP (skill was not run this session, but a tool call is happening):**
the FIRST substantive tool-call response in that session carries a
postscript:

```
(Preflight not run this session.)
```

This postscript is invisible-by-design until it appears. Its appearance
is the signal that the gate failed to fire. Sean can then call the next
session fresh.

---

## 4. Skill self-knowledge

The skill is allowed to:

- Fetch the canonical files listed above
- Read `console/locked-rules.md` for the confirmation list
- Print the PASS/PARTIAL/FAIL/SKIP output exactly as specified

The skill is NOT allowed to:

- Block any tool call on its own. PASS is silent, FAIL still proceeds.
- Mutate auto-memory or the repo. It is read-only at the file system.
- Run any per-page check that belongs to `lesaruss-preflight`,
  `ada-checker`, `lesaruss-internal-page`, or `lesaruss-public-page`.
  Those skills own their respective gates.

---

## 5. Future scope

Day 1 is fetch verification. Likely Day 2+ additions, in order of
expected lock-in:

- Verify the deploy token (.deploy-token) is readable for the active
  station before any push attempt.
- Confirm the locked HTML template files are present on disk before any
  internal-page or public-page creation.
- Confirm the active brand cartridge matches the working folder before
  any brand-specific output.
- Print a one-line cohort summary on session start when the conversation
  context references three or more brands (currently silent).

Each addition lands as a new sub-section here with its own LOCKED date,
following the same scope-narrow-first pattern that rule 1.7 used.

---

## 6. Why this skill exists

The 2026-05-05 conversation: Sean asked "how can we work where you don't
make mistakes." Diagnosis: the same canonical rules are sometimes loaded
and sometimes not, depending on whether Claude follows the project-
instructions fetch step at session start. The fetch step is a soft
default, not a hard gate. The result is silent rule-dropping that surfaces
later as drift, which costs round trips to fix.

This skill is the hard gate. Skills can be invoked. The fetch step
cannot be skipped silently anymore because the absence of the skill's
silent PASS produces a visible SKIP postscript on the very next
substantive output.

The fix to the original problem ("how can I work with you where you
don't make mistakes") is two-part:
1. Make the preflight a hard gate (this skill).
2. Each new mistake gets a postmortem before the fix: was this a new
   variable or a repeat? If repeat, fix the rule infrastructure before
   fixing the mistake. (Tracked separately as the third lever in the
   2026-05-05 conversation.)

This skill is the first lever. It does not eliminate new mistakes. It
eliminates the silent recurrence of rules-already-locked-but-not-loaded.
