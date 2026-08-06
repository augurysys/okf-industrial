---
okf_version: "0.2"
---

# Northfield Facility — Slurry Feed Line 1 (showcase bundle)

> **All content in this bundle is fictional.** GlobalMetals Corp, the Northfield Facility, every asset, tag, person, email, note, date, and endpoint below is invented to demonstrate the OKF Industrial Profile. There is no real plant, no real person, and no real operational data here. Standards are referenced by name only; nothing is reproduced from any standards document.

This bundle captures the operational and human knowledge of one fictional production line — Slurry Feed Line 1 in Refining Section B — as human-verified, sourced knowledge an AI agent can safely use.

**Read it cold in this order:** this index → the pump [P-101A](/assets/slurry-charge-pump-101a.md) → the [stale-transmitter email](/references/email-stale-transmitter-incident.md) → the [change log](/log.md). That path alone tells the provenance story: an incident happened, a claim was reviewed, a rule was adopted, and agent behavior followed.

## Directory

### Bundle root

- [`AGENTS.md`](/AGENTS.md) — How an AI agent must read and use this bundle: resolve tags, check liveness, obey the trust policy and review status, and never merge knowledge.
- [`log.md`](/log.md) — Date-grouped history of how this bundle's knowledge changed, newest first.
- [`tag-directory.md`](/tag-directory.md) — The registry binding every instrument tag to the asset and declared stream it belongs to; the single place an agent resolves a tag.
- [`relations.md`](/relations.md) — Typed edges between Northfield entities: material flow, composition, and one operator-observed lead/lag.
- [`learned.md`](/learned.md) — The staging area for facts proposed by the triage assistant: one pending observation awaiting review, one claim rejected with the engineer's reason.

### Assets

- [`assets/slurry-charge-pump-101a.md`](/assets/slurry-charge-pump-101a.md) — Slurry charge pump feeding the primary clarifier; carries a stale-reading trust policy and the confirmed cold-start heuristic.
- [`assets/clarifier-feed-motor-201.md`](/assets/clarifier-feed-motor-201.md) — Motor driving clarifier recirculation; its recirculation changes are the observed leading indicator for TK-101 level.
- [`assets/clarifier-tank-101.md`](/assets/clarifier-tank-101.md) — Static vessel receiving slurry from P-101A; deliberately minimal, to show the profile is not limited to rotating equipment.
- [`assets/slurry-feed-line-1.md`](/assets/slurry-feed-line-1.md) — The production line treated as a first-class asset; declares the batch-system phase indication it references but never models.

### Heuristics

- [`heuristics/pump-101a-cold-start.md`](/heuristics/pump-101a-cold-start.md) — On cold winter starts, a brief inlet-pressure dip on P-101A clears on its own; a short wait distinguishes it from a real fault.
- [`heuristics/clarifier-settling-phase.md`](/heuristics/clarifier-settling-phase.md) — During the SETTLE phase of CLARIFY-01 the feed is deliberately reduced, so low flow on P-101A is expected and a flow alarm in that phase is not a fault.

### Policies

- [`policies/safe-agent-actions.md`](/policies/safe-agent-actions.md) — Conditions that must hold before an agent recommends (never executes) an intervention; limits are referenced by identifier, never by value.

### Skills

- [`skills/vibration-triage.md`](/skills/vibration-triage.md) — A runbook for triaging a vibration or bearing indication on the line's rotating equipment, using streams, the tag directory, relations, and the trust policy.

### References (ground-truth documents)

- [`references/shift-handover-cold-start.md`](/references/shift-handover-cold-start.md) — Millwright's handover note describing the winter cold-start inlet-pressure dip on P-101A and the wait that tells it apart from a real fault.
- [`references/email-stale-transmitter-incident.md`](/references/email-stale-transmitter-incident.md) — Process engineer's email after a frozen bearing-temperature reading nearly caused a healthy pump to be tripped; asks for a standing trust window.
- [`references/reliability-review-minutes.md`](/references/reliability-review-minutes.md) — Minutes recording the operator-observed lead/lag between M-201 recirculation changes and TK-101 level, and the decision to record it as an observation, not a prediction.
- [`references/process-note-settling-phase.md`](/references/process-note-settling-phase.md) — Process engineer's note explaining that reduced P-101A flow during the settling phase of clarification is deliberate, and flow alarms in that phase are not faults.
