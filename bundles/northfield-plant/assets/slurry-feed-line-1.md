---
type: Asset
title: "Slurry Feed Line 1 (LINE-1)"
description: "The production line treated as a first-class asset; declares the batch-system phase indication it references but never models."
resource: /assets/slurry-feed-line-1.md
tags: [LINE-1, production-line, Refining-Section-B, process]
generated: { by: human:rokafor, at: 2026-04-08T10:00:00Z }
verified:
  - { by: human:rokafor, at: 2026-04-08T10:00:00Z }
status: stable
telemetry_streams:
  line_phase: { tag: YC-101-PHASE, resource: "opc.tcp://edge.northfield.example/LINE1/phase" }
sources:
  - id: procedure-clarify-01
    resource: "batch://northfield.example/procedures/CLARIFY-01"
    standard: ISA-88
    system: "Batch system"
    title: "Clarification procedure CLARIFY-01 (owned by the batch system)"
  - id: settle-phase
    resource: "batch://northfield.example/procedures/CLARIFY-01/SETTLE"
    standard: ISA-88
    system: "Batch system"
    title: "Settling phase of clarification procedure CLARIFY-01"
---

# Slurry Feed Line 1 (LINE-1)

## Overview

Slurry Feed Line 1 is a production line in Refining Section B, treated here as a first-class asset. Its three machines — the charge pump P-101A, the clarifier feed motor M-201, and the clarifier tank TK-101 — are `PART_OF` this line; see [Relations](/relations.md). Treating the line as an asset is what lets the profile carry *process* judgment, not only machine judgment.

## Phase is referenced, never modeled

The line runs a clarification procedure the batch system knows as CLARIFY-01, which moves through phases including a settling phase, SETTLE.[^procedure-clarify-01][^settle-phase] Those phase identities belong to the batch system. This asset declares a single stream, `line_phase` (tag `YC-101-PHASE`), which is the endpoint where the batch system's current phase indication is read at decision time.

What this file deliberately does **not** contain:

- No list of the line's phases and no ordering of them.
- No state machine, no transitions, no recipe, and no phase definitions.
- No feed setpoints or flow values for any phase.

The profile only *references* the phase identifiers through `sources[]`; the live phase value is the batch system's, read from the declared stream when a decision is being made. Knowledge scoped to a phase — for example that low P-101A flow is expected during SETTLE — lives in a heuristic that binds to this stream through `applies_when`; see [`/heuristics/clarifier-settling-phase.md`](/heuristics/clarifier-settling-phase.md).

## Related context

- Member assets: [P-101A](/assets/slurry-charge-pump-101a.md), [M-201](/assets/clarifier-feed-motor-201.md), [TK-101](/assets/clarifier-tank-101.md)
- Scoped process heuristic: [`/heuristics/clarifier-settling-phase.md`](/heuristics/clarifier-settling-phase.md)
- Relationships: [`/relations.md`](/relations.md)

[^procedure-clarify-01]: Clarification procedure CLARIFY-01, owned by the batch system. `batch://northfield.example/procedures/CLARIFY-01`
[^settle-phase]: Settling phase of clarification procedure CLARIFY-01. `batch://northfield.example/procedures/CLARIFY-01/SETTLE`
