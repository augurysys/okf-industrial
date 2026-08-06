---
type: Asset
title: "Slurry Charge Pump P-101A"
description: "Slurry charge pump feeding the primary clarifier; carries a stale-reading trust policy and the confirmed cold-start heuristic."
resource: /assets/slurry-charge-pump-101a.md
tags: [P-101A, pump, rotating-equipment, Refining-Section-B]
generated: { by: human:rokafor, at: 2026-03-20T09:10:00Z }
verified:
  - { by: human:rokafor, at: 2026-03-20T09:10:00Z }
status: stable
telemetry_streams:
  vibration:       { tag: VT-101A-DE,  resource: "opc.tcp://edge.northfield.example/P101A/vibration" }
  bearing_temp:    { tag: TT-101A-BRG, resource: "historian://pi.northfield.example/P101A_BRG_TEMP" }
  flow:            { tag: FT-101A,     resource: "historian://pi.northfield.example/P101A_FLOW" }
  inlet_pressure:  { tag: PT-101A-IN,  resource: "opc.tcp://edge.northfield.example/P101A/inlet_pressure" }
trust_policy:
  trust_window_minutes: 30
  when_stale: >
    Treat the reading as failed, not as data. Conclusions that depend on it are
    advisory-only. Never take a control action based on a stale reading; verify
    at the transmitter and the local gauge first.
  source: email-stale-transmitter
  verified: { by: human:rokafor, at: 2026-03-20T09:00:00Z }
tribal_knowledge:
  - claim: "On cold winter starts, P-101A shows a brief inlet-pressure dip that clears on its own once the intake-valve grease warms; a short wait tells it apart from a real fault."
    contributor: human:jmiller
    contributor_certification: "ISO 18436-2 Category II vibration analyst"
    source: handover-cold-start
    quote: "Give it about 90 seconds; if the pressure comes back on its own, it's the grease, not a fault. Don't trip a healthy pump inside that first minute and a half."
    confidence: high
    review_status: confirmed
    canonical: /heuristics/pump-101a-cold-start.md
sources:
  - id: dcs-vib-trip-p101a
    resource: "opc.tcp://dcs.northfield.example/limits/P101A.VibHigh"
    standard: ISA-95
    system: DCS
    title: "P-101A high-vibration trip limit (value owned by the DCS)"
  - id: handover-cold-start
    resource: /references/shift-handover-cold-start.md
    title: "Shift handover note — cold-start pressure dip"
  - id: email-stale-transmitter
    resource: /references/email-stale-transmitter-incident.md
    title: "Email — overnight phantom bearing alarm (stale transmitter)"
---

# Slurry Charge Pump P-101A

## Operational overview

P-101A is the slurry charge pump for Slurry Feed Line 1 in Refining Section B. It draws slurry from the section feed header and delivers it toward the primary clarifier tank TK-101. It is a rotating machine on continuous duty, monitored for drive-end vibration, bearing temperature, discharge flow, and inlet pressure. All four are declared as telemetry streams above and resolve through the [Tag Directory](/tag-directory.md); the pump's place in the process is described in [Relations](/relations.md).

## Trust and stale readings

This asset carries a trust policy: a reading that has not refreshed within the trust window is treated as failed, not as data. The window and the rule exist because a frozen bearing-temperature reading once nearly caused a healthy pump to be tripped in the dark.[^email-stale-transmitter] When a reading is stale, any conclusion that depends on it is advisory-only, and no control action should be recommended on the strength of it — verify at the transmitter and the local gauge first. Liveness is checked live at the endpoint at decision time; this file never stores a current value or a last-seen time.

## Safety and agent actions

Before any intervention is *recommended* (never executed) against this pump, the gating conditions in [`/policies/safe-agent-actions.md`](/policies/safe-agent-actions.md) must hold. Engineered trip and alarm limits are owned by the DCS and are referenced by identifier only[^dcs-vib-trip-p101a] — their values are never copied here.

## Cold-start behavior

On cold winter starts P-101A shows a brief inlet-pressure dip that clears on its own as the intake-valve grease warms. The short wait that distinguishes this from a real fault is the confirmed cold-start heuristic, summarized above and owned canonically at [`/heuristics/pump-101a-cold-start.md`](/heuristics/pump-101a-cold-start.md).[^handover-cold-start]

## Known failure modes (ISO 14224 vocabulary)

Named using ISO 14224 failure-mode vocabulary, with qualitative symptoms only — no numeric thresholds live here; the DCS owns the limits.

- **`bearing_failure` (wear / spalling):** rising drive-end vibration and bearing temperature trending together, often with an audible roughness at the DE. Confirm liveness of both readings before drawing a conclusion.
- **`impeller_wear` (erosion):** gradual loss of delivered flow at similar drive conditions; a slow drift rather than a step change.
- **`seal_leakage`:** visible weep at the seal and, sometimes, erratic inlet-pressure behavior unrelated to the cold-start dip.

Symptoms are qualitative cues for triage, not decision limits. The decision limits are the DCS's.

## Related context

- Heuristic: [`/heuristics/pump-101a-cold-start.md`](/heuristics/pump-101a-cold-start.md)
- Line context: [`/assets/slurry-feed-line-1.md`](/assets/slurry-feed-line-1.md)
- Downstream: [`/assets/clarifier-tank-101.md`](/assets/clarifier-tank-101.md)
- Triage runbook: [`/skills/vibration-triage.md`](/skills/vibration-triage.md)
- Source documents: the [handover note](/references/shift-handover-cold-start.md) and the [stale-transmitter email](/references/email-stale-transmitter-incident.md)

[^handover-cold-start]: Shift handover note — cold-start pressure dip. `/references/shift-handover-cold-start.md`
[^email-stale-transmitter]: Email — overnight phantom bearing alarm (stale transmitter). `/references/email-stale-transmitter-incident.md`
[^dcs-vib-trip-p101a]: P-101A high-vibration trip limit, value owned by the DCS. `opc.tcp://dcs.northfield.example/limits/P101A.VibHigh`
