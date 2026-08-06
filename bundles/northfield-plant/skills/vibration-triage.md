---
type: Skill
title: "Vibration triage for P-101A / M-201"
description: "A runbook for triaging a vibration or bearing indication on the line's rotating equipment, using streams, the tag directory, relations, and the trust policy."
resource: /skills/vibration-triage.md
tags: [triage, vibration, runbook, P-101A, M-201]
generated: { by: human:rokafor, at: 2026-05-12T10:30:00Z }
verified:
  - { by: human:rokafor, at: 2026-05-12T10:30:00Z }
status: stable
---

# Vibration triage for P-101A / M-201

## When to use

Use this when a vibration or bearing indication is raised on a rotating machine of Slurry Feed Line 1 — the charge pump P-101A or the clarifier feed motor M-201 — and you need to decide whether it is an expected pattern, a data problem, or a genuine fault worth escalating.

## Preconditions

- You can resolve the machine's tags through the [tag directory](/tag-directory.md).
- You can check stream liveness at the endpoints named there.
- You have read the machine's asset file and any heuristics it references.

## Steps

1. **Resolve the tags.** Look up the vibration and bearing-temperature tags for the machine in the [tag directory](/tag-directory.md) — for P-101A, `VT-101A-DE` and `TT-101A-BRG`. Do not guess an endpoint.
2. **Check liveness first.** Confirm each reading is live within the machine's trust window. If a reading is stale, apply the [trust policy](/assets/slurry-charge-pump-101a.md): treat it as failed, make any conclusion advisory-only, and recommend no control action — direct a human to check the transmitter and local gauge.
3. **Rule out expected behavior.** Before calling anything a fault, exclude known patterns: a [cold-start inlet-pressure dip](/heuristics/pump-101a-cold-start.md) after a cold start, or [expected low flow during SETTLE](/heuristics/clarifier-settling-phase.md) if the line is in that phase (read the phase from `line_phase`).
4. **Look up and downstream.** Use [`/relations.md`](/relations.md) to see what is connected: P-101A flows to TK-101, and M-201 has an operator-observed lead on TK-101 level. Use these to decide where else to look — not to forecast one signal from another.
5. **Compare against the owned limits by reference.** Any comparison to a trip or alarm limit refers to the DCS-owned identifier; this runbook states no thresholds. The limit value belongs to the DCS.
6. **Decide and hand off.** If expected patterns are ruled out, inputs are live, and the indication persists, escalate to a human with your reasoning and citations. Recommend; do not execute.

## Post-conditions

- The indication is classified as expected pattern, stale/failed data, or a candidate fault.
- Every conclusion cites the confirmed claim, stream, or relation it rests on.
- If any input was stale, the output is marked advisory-only and no control action was recommended.
- Any control decision is left to a human.
