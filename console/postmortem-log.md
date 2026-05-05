# Postmortem Log

**Owner:** Sean A. Russell
**Started:** 2026-05-05
**Purpose:** Empirical record of every REPEAT detected by the `lesaruss-mistake-postmortem` skill. Each line is one detection, with the rule reference, the rule-infrastructure change made, and the trigger phrase (or self-detection note). Used for calibrating the visibility sunset clause in rule 1.9 and for spotting which rules are most-violated.

> Why this file exists: rule 1.9 fires every time a mistake is corrected. Without an empirical record, "is the gate working" becomes a vibes question. With a record, the answer is "look at the log." The log also feeds into `consolidate-memory` and any future audit skill.

## Format

```
- YYYY-MM-DD: Rule X.Y. [What changed in the rule infrastructure.] (Trigger: [user phrase or self-detection note].)
```

Meta-failures (rule 1.7 or 1.8 itself failing to fire) get the prefix `META:` and are surfaced to Sean immediately rather than auto-repaired.

## Calibration thresholds (from rule 1.9, section 5)

- More than 3 REPEATs per session on average over 2 weeks: trigger is too broad, narrow it.
- Fewer than 1 REPEAT per week and Sean has stopped checking: switch to silent on REPEAT, log only.
- 1 to 3 REPEATs per week and Sean is still checking: keep visible.

## Log

