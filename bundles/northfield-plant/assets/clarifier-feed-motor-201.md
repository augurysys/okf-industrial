---
type: Asset
title: "Clarifier Feed Motor M-201"
description: "Motor driving clarifier recirculation; its recirculation changes are the observed leading indicator for TK-101 level."
resource: /assets/clarifier-feed-motor-201.md
tags: [M-201, motor, rotating-equipment, Refining-Section-B]
generated: { by: human:rokafor, at: 2026-02-20T16:00:00Z }
verified:
  - { by: human:rokafor, at: 2026-02-20T16:00:00Z }
status: stable
telemetry_streams:
  vibration_nde: { tag: VT-201-NDE, resource: "opc.tcp://edge.northfield.example/M201/vibration_nde" }
  stator_temp:   { tag: TT-201-STA, resource: "historian://pi.northfield.example/M201_STATOR_TEMP" }
  line_current:  { tag: IT-201,     resource: "historian://pi.northfield.example/M201_LINE_CURRENT" }
sources:
  - id: reliability-review-minutes
    resource: /references/reliability-review-minutes.md
    title: "Reliability review minutes — M-201 / TK-101 lead-lag"
---

# Clarifier Feed Motor M-201

## Operational overview

M-201 drives the clarifier recirculation on Slurry Feed Line 1 in Refining Section B. It is monitored for non-drive-end vibration, stator temperature, and line current; all three are declared as telemetry streams above and resolve through the [Tag Directory](/tag-directory.md).

## Leading-indicator context

Operators have long noticed that when M-201 recirculation is changed, the level at TK-101 follows a while later. This is recorded as an operator-observed `LEADS` edge in [Relations](/relations.md), sourced to the reliability review minutes.[^reliability-review-minutes] It is an *observation*, not a prediction: both signals track feed rate, so the relationship is treated as a shared-cause correlation, not evidence that M-201 drives TK-101. An agent may raise it as a place to look, never as a forecast.

## Known failure modes (ISO 14224 vocabulary)

Qualitative cues only; engineered limits belong to the systems that own them.

- **`insulation_degradation`:** stator temperature drifting up at comparable load and cooling conditions.
- **`bearing_failure` (wear):** rising non-drive-end vibration, often with a change in the current signature.

## Related context

- Line context: [`/assets/slurry-feed-line-1.md`](/assets/slurry-feed-line-1.md)
- Downstream tank: [`/assets/clarifier-tank-101.md`](/assets/clarifier-tank-101.md)
- Relationships: [`/relations.md`](/relations.md)
- Source document: [reliability review minutes](/references/reliability-review-minutes.md)

[^reliability-review-minutes]: Reliability review minutes — M-201 / TK-101 lead-lag. `/references/reliability-review-minutes.md`
