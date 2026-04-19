# The Signal — LESARUSS Central Intelligence

**The Signal** is the master knowledge base for the entire LESARUSS universe. It is the source of truth that all AI tools, agents, and stations tap into.

## What It Is
A public GitHub repository (`lesaruss/lesaruss-context`) that any AI tool with internet access can fetch via raw.githubusercontent.com URLs. Contains the LESARUSS org chart, brand context, standards, terminology, and active project state.

## Key Principle
The Signal is AI-agnostic. Claude powers it today. That may change. The Signal outlasts any one AI provider.

---

## PULSE — Communication Layer

PULSE is how anything communicates with The Signal. It is tiered by access level:

| Tier | Who | What | Status |
|------|-----|------|--------|
| v1 (100% Sean only) | Sean personally | iMessage to V Station + Fieldy voice memos | Live as of 2026-04-19 |
| 25% | Members | Community chatbot | Planned |
| 50% | Members | Advanced chatbot | Planned |
| 75% | Members + Clients | The Huddle (web-based meeting room, phone-accessible) | In design |
| 100% (future) | Everyone | Own AI infrastructure, own servers, own models | Future |

---

## Fieldy = PULSE v1

Fieldy is the proof of concept for PULSE. The loop:
1. Sean speaks into a voice memo
2. Fieldy transcribes it
3. v-fieldy-report task processes it into the Sean Report
4. Summary gets committed to The Signal

The real PULSE product will be built with LESARUSS's own technology based on what Fieldy proves out.

---

## PULSE Device
The PULSE Flagband Bluetooth device is a physical wearable. Not an Apple Watch. Represents the personal always-on tier. Future: hardware interface directly into The Signal.

---

## V Station Connection
The Mac Mini V Station runs autonomously 24/7. The iMessage bridge (Sean texts V directly via Apple Messages) is PULSE v1's personal channel. Sean's exclusive access. Members access The Signal through the chatbot tier.

---

## Session-to-Signal Pipeline (Target State)
Every Cowork session should output a summary committed to this repo. Currently manual. Target: automated write-back so The Signal stays current in real time without Sean having to think about it.

---

## The Distinction

| Term | What It Is |
|------|-----------|
| The Signal | The brain. Static until updated. The GitHub repo. |
| PULSE | The heartbeat. Constant rhythm of updates feeding The Signal. |
| Fieldy | How Sean's voice becomes a PULSE. PULSE v1. |
| Scheduled tasks | How agents send automatic PULSEs. |
| iMessage bridge | How Sean communicates directly with The Signal via V. |

---

*Locked: 2026-04-19. Named by Sean A. Russell.*
