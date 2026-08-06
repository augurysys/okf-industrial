---
type: Heuristic
title: "P-101A cold-start inlet-pressure dip"
description: "On cold winter starts, a brief inlet-pressure dip on P-101A clears on its own; a short wait distinguishes it from a real fault."
resource: /heuristics/pump-101a-cold-start.md
tags: [P-101A, cold-start, inlet-pressure, PT-101A-IN]
generated: { by: human:rokafor, at: 2026-02-20T15:45:00Z }
verified:
  - { by: human:rokafor, at: 2026-02-20T15:45:00Z }
status: stable
claim: "On a cold winter start, P-101A shows a brief inlet-pressure dip that clears on its own as the intake-valve grease warms; waiting about 90 seconds distinguishes this expected behavior from a real fault."
contributor: human:jmiller
contributor_certification: "ISO 18436-2 Category II vibration analyst; 24 years on this equipment"
source: handover-cold-start
quote: "Give it about 90 seconds; if the pressure comes back on its own, it's the grease, not a fault. Don't trip a healthy pump inside that first minute and a half."
confidence: high
review_status: confirmed
sources:
  - id: handover-cold-start
    resource: /references/shift-handover-cold-start.md
    title: "Shift handover note — cold-start pressure dip"
---

# P-101A cold-start inlet-pressure dip

This is the canonical home of the cold-start claim; the pump asset summarizes it and points here.

## The judgment

On a cold winter start, P-101A shows a brief inlet-pressure dip on `PT-101A-IN` right after the pump comes up. It happens because the intake-valve grease is still stiff and warming; it is not a fault. The dip clears on its own. A short wait — about 90 seconds — is what tells this expected behavior apart from a genuine low-pressure problem.[^handover-cold-start]

The ~90-second wait is the one quantity this heuristic owns. It has no other system of record, so it is written here as a policy parameter, and it carries its receipt: the millwright's handover note quoted above. It is a *wait*, not an engineered pressure limit — the pressure trip and alarm limits themselves belong to the DCS and are referenced, never stated.

## How to use it

- Confirm the start was genuinely cold (winter morning, cold ambient) and the pump has only just started.
- Confirm `PT-101A-IN` is a live reading, not a stale one — apply the pump's [trust policy](/assets/slurry-charge-pump-101a.md) first.
- Wait the short cold-start interval. If inlet pressure recovers on its own, this is the grease, not a fault, and no action is warranted.
- If pressure stays down after the wait, or the drive-end bearing sounds rough, escalate and treat it as a possible real fault. Log ambient temperature and the exact start time.

## Provenance

Contributed by the lead millwright and quoted verbatim from the shift-handover note. Reviewed and confirmed by the reliability engineer on 20 Feb 2026 (`review_status: confirmed`). See [`log.md`](/log.md) for the review arc.

[^handover-cold-start]: Shift handover note — cold-start pressure dip. `/references/shift-handover-cold-start.md`
