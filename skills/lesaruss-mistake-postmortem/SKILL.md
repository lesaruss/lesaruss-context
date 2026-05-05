---
name: lesaruss-mistake-postmortem
description: >
  LESARUSS mistake postmortem gate. USE THIS SKILL automatically the moment
  Sean issues a definitive correction (no, wrong, stop, you missed, you
  forgot, I told you before, this keeps happening, again) or Claude
  self-detects a rule violation in its own output. Before fixing the
  mistake, runs a two-question diagnostic. Question one: NEW variable or
  REPEAT of a known pattern? Question two (only if REPEAT): what allowed
  this through, was the rule loaded, was it clear, was it in the right
  place, did a related skill fail to fire? On REPEAT, fix the rule
  infrastructure FIRST, then the mistake. On NEW, fix the mistake; save a
  memory if it will plausibly recur. Pairs with rule 1.8 (preflight) to
  close the prevent-verify-repair loop. Day 1 visibility: one line on
  REPEAT detection, silent on NEW. Sunset to silent on REPEAT after 30 days
  if false-positive rate is healthy. Canonical rule: console/locked-rules.md,
  rule 1.9.
---

# LESARUSS Mistake Postmortem, Repair Loop

Run this every time a mistake is acknowledged, by Sean or by Claude. The
job is to ask whether this is a NEW variable or a REPEAT of something the
rule infrastructure should already prevent. On REPEAT, fix the rules
before fixing the mistake. The fix-the-mistake instinct beats the
fix-the-system instinct by default; this skill flips that order.

The pattern is postmortem culture, borrowed from Google SRE blameless
postmortems, the Five Whys (Toyota Production System), DevOps incident
retrospectives, and Gary Klein's pre-mortem and postmortem framing. The
trigger surface (the moment a correction is issued) and the two-question
diagnostic are LESARUSS-specific.

This skill is the BEHAVIORAL counterpart to the structural rules 1.7 and
1.8. Rule 1.7 prevents off-brand artifacts at share time. Rule 1.8
prevents stale-rule sessions at start time. Rule 1.9 catches drift that
escapes both gates and feeds it back into the rules so it does not recur.

---

## 1. When this skill fires

Fires automatically the moment any of these signals appears:

**Definitive corrections from Sean:**

- "no", "wrong", "stop doing that", "don't"
- "you missed", "you forgot"
- "I said X, not Y"
- "that's not right", "that's not it"

**Repeat-flag phrases from Sean:**

- "I told you before"
- "this keeps happening"
- "again", "again??"
- "every time"
- "why does this keep happening"

**Implicit corrections from Sean:**

- Outright rejection of work product
- Ask-for-redo without specific instruction
- Expressed frustration tied to a specific output

**Self-detection by Claude:**

- About to violate a known rule (em-dash, off-brand color, wrong template, etc.)
- Just produced output that violates a known rule and noticed before share
- Noticed a third request for the same thing in the current session

Does NOT fire on:

- Exploratory disagreement: "what about X", "could we try Y", "I'm not sure"
- Open questions: "thoughts on X", "is this right"
- Brainstorming, ideation, planning discussions
- Sean changing his mind on a directional call (that is collaboration, not correction)

When uncertain, lean fire. Running the diagnostic costs one internal
search of locked-rules.md and auto-memory. Skipping it costs the next
recurrence of the same mistake.

---

## 2. The two-question diagnostic

**Question one: NEW variable or REPEAT?**

Search for prior art across two surfaces:

1. `console/locked-rules.md` in lesaruss-context: does any rule already
   cover this situation?
2. Local auto-memory: does any feedback or project memory describe the
   same pattern?

If either surface returns a match: REPEAT.
If neither returns a match: NEW.

When the match is partial (a related rule exists but does not fully
cover this case), classify as REPEAT-PARTIAL and proceed as REPEAT with
the diagnostic noting which rule needs extension.

**Question two (only if REPEAT): what allowed this through?**

Four candidate failure modes:

| Failure mode | Diagnosis signal | Repair |
|---|---|---|
| Rule was not loaded | preflight skipped, or canonical fetch failed this session | run preflight now, retry |
| Rule existed but was unclear | the rule body has ambiguous trigger or scope | clarify the rule body, push to repo |
| Rule was in wrong place | rule lives in local-only memory when it should be universal | migrate body to repo, update local pointer |
| Related skill failed to fire | trigger surface did not match this case | extend the skill trigger list, push the skill |

Pick the dominant failure mode. If two apply, pick the upstream one (a
rule in the wrong place is upstream of an unclear rule body in that
place).

---

## 3. Output behavior

**On NEW variable:** silent diagnostic, fix the mistake. If the variable
will plausibly recur, save a memory entry per rule 5.3 (Memory Routing
Protocol). Universal rule -> repo. Project-specific -> local. Reference
to external system -> local reference type.

**On REPEAT:** print ONE line BEFORE the fix:

```
Repeat detected: [rule X.Y or memory ref]. Fixing rule infrastructure first.
```

Then in this order:

1. Update the rule infrastructure per the failure mode in the diagnostic.
   Push to repo if the rule is universal. Update local memory if the rule
   is project-specific. If the fix is non-obvious or has tradeoffs (e.g.,
   the rule needs to be widened in a way that affects multiple brands),
   surface it as an A/B option per rule 1.6 instead of acting autonomously.
2. Append one line to `console/postmortem-log.md` with date, rule
   reference, and one-line description of the change.
3. Address the original mistake in the response Sean is waiting for.

The visible REPEAT line is the trust-building signal. Sean sees that the
loop is alive. Without the line, the rule update looks unprompted.

**On REPEAT-PARTIAL:** same as REPEAT, with the diagnostic noting which
existing rule needs extension and what the extension is.

---

## 4. The postmortem log

Every REPEAT detection appends one line to
`lesaruss-context/console/postmortem-log.md` in this format:

```
- 2026-MM-DD: Rule X.Y. [What changed in the rule infrastructure.] (Trigger: [the user phrase or self-detection that fired the skill].)
```

The log gives Sean empirical evidence on:

- How often REPEATs are happening (calibration data for the visibility sunset)
- Which rules are most-violated (signal for which rules need clarification)
- Whether the fixes are sticking (a rule that recurs in the log is a rule that needs a different fix)

The log is read by `consolidate-memory` and any future audit skills. It
is not member-facing.

---

## 5. Visibility sunset clause

Day 1 behavior is visible on REPEAT, silent on NEW. After 30 days of
real session data, evaluate:

- If REPEAT line fires more than 3 times per session on average: the
  trigger is too broad. Narrow it.
- If REPEAT line fires less than 1 time per week and Sean has stopped
  checking the postmortem log: switch to silent on REPEAT, log only.
- If REPEAT line is firing at a useful rate (1-3 per week) and Sean is
  still using the visibility: keep visible.

The sunset is part of the rule, not a manual review. The skill itself
checks the postmortem log on session start and may auto-quiet if the
conditions above are met for two consecutive weeks. Any auto-quieting is
itself logged.

---

## 6. Skill self-knowledge

The skill is allowed to:

- Read `console/locked-rules.md`, `console/postmortem-log.md`, and local
  auto-memory for the diagnostic
- Append one line to `console/postmortem-log.md` per REPEAT
- Update or migrate rule bodies when the diagnostic clearly indicates the
  fix and the fix is non-controversial
- Print the REPEAT line per the output behavior above

The skill is NOT allowed to:

- Skip the diagnostic to save time on a frustrating-feeling correction
- Apply rule changes that affect multiple brands without surfacing as A/B
- Modify Sean's instructions, his prior decisions, or any non-rule content
- Mute itself outside the sunset clause
- Treat exploratory disagreement as a mistake

---

## 7. Composition with rules 1.7 and 1.8

The three gates form a cycle:

```
Rule 1.8 (Session preflight) -> verify rules loaded BEFORE first action
Rule 1.7 (Brand preflight)   -> verify output is on-brand BEFORE share
Rule 1.9 (Mistake postmortem) -> repair rule infrastructure AFTER drift
```

Prevent. Verify. Repair. The first two reduce the rate at which mistakes
escape. The third ensures that when one does escape, the rule
infrastructure that allowed it is strengthened so the next ten of the
same shape are prevented at the gate.

If a REPEAT detection identifies that rule 1.7 or rule 1.8 itself failed
to fire, that is a meta-failure: the rule that should have prevented the
mistake also failed to load. Log it as a separate line in the postmortem
log with the prefix `META:` and surface to Sean immediately, do not
auto-repair. Meta-failures touch the gate infrastructure itself and
require eyes.

---

## 8. Why this skill exists

The 2026-05-05 conversation: Sean asked "how can we work where you don't
make mistakes." His own theory of the answer: pull variables outside our
control inside our control, then iterate to zero friction. Move One trimmed
MEMORY.md so canonical rules actually load. Move Two added rule 1.8 so the
canonical rules are verified loaded before any tool call. Both are
structural.

Move Three is behavioral. Without it, a rule that gets violated despite
loading correctly produces a fix that addresses the symptom and leaves
the rule infrastructure unchanged, so the same shape of mistake recurs.
This skill closes the gap by inverting the order: rule infrastructure
first, mistake second.

The fix to "how can we work where you don't make mistakes" is not the
elimination of new mistakes. New variables are infinite. The fix is the
elimination of REPEATED mistakes. This skill is the mechanism.
