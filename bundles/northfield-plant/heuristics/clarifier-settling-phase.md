---
type: Heuristic
title: "Low P-101A flow during the SETTLE phase is expected"
description: "During the SETTLE phase of CLARIFY-01 the feed is deliberately reduced, so low flow on P-101A is expected and a flow alarm in that phase is not a fault."
resource: /heuristics/clarifier-settling-phase.md
tags: [P-101A, LINE-1, SETTLE, CLARIFY-01, flow, FT-101A]
generated: { by: human:rokafor, at: 2026-04-08T10:10:00Z }
verified:
  - { by: human:rokafor, at: 2026-04-08T10:10:00Z }
status: stable
claim: "During the SETTLE phase of CLARIFY-01, a low-flow indication on P-101A is expected because feed is deliberately reduced; a flow alarm in that phase is not a pump fault."
contributor: human:dreyes
source: process-note-settling-phase
quote: "During SETTLE on CLARIFY-01 we back the feed right down on purpose, so a low-flow indication on P-101A in that phase is expected behavior, not a fault."
confidence: high
review_status: confirmed
applies_when:
  phase: SETTLE
  phase_stream: line_phase
sources:
  - id: process-note-settling-phase
    resource: /references/process-note-settling-phase.md
    title: "Process note — low flow during SETTLE is expected"
  - id: settle-phase
    resource: "batch://northfield.example/procedures/CLARIFY-01/SETTLE"
    standard: ISA-88
    system: "Batch system"
    title: "Settling phase of clarification procedure CLARIFY-01"
---

# Low P-101A flow during the SETTLE phase is expected

## The judgment

During the SETTLE phase of the clarification procedure, the slurry feed is deliberately reduced so the clarifier can settle. A low-flow indication on P-101A during that phase is expected behavior, not a fault, and a flow alarm in that window is telling you the phase is doing its job.[^process-note-settling-phase] Outside SETTLE, low flow on P-101A means what it usually means and should be investigated.

## The boundary — who owns the phase

The batch system owns the phase. This file owns only the *judgment* about how to read a low-flow indication while that phase is active. The heuristic is scoped with `applies_when`: it applies only when `phase: SETTLE`, and whether the line is actually in SETTLE is read live from the `line_phase` stream (tag `YC-101-PHASE`) declared on [`/assets/slurry-feed-line-1.md`](/assets/slurry-feed-line-1.md). The phase's identity is crosswalked through `sources[]` to the batch system.[^settle-phase]

No feed setpoints or flow values appear here. Those live in the recipe, in the batch system, and change with it. Copying them would make this file wrong the next time the recipe changes.

## How an agent should use it

- Read the current phase from `line_phase` at decision time. Do not assume it.
- If — and only if — the line is in SETTLE, treat a low-flow indication or flow alarm on P-101A as expected, and say so rather than raising a pump fault.
- If the line is not in SETTLE, this heuristic does not apply; handle low flow normally.

## Provenance

Contributed by process engineering and quoted verbatim from the process note. Reviewed and confirmed by the reliability engineer (`review_status: confirmed`).

[^process-note-settling-phase]: Process note — low flow during SETTLE is expected. `/references/process-note-settling-phase.md`
[^settle-phase]: Settling phase of clarification procedure CLARIFY-01. `batch://northfield.example/procedures/CLARIFY-01/SETTLE`
