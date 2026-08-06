# Change log — Northfield plant bundle

History of how this bundle's knowledge changed, newest first. Each entry is a step in the provenance story: an incident happens, a claim is proposed, a human reviews it, and a rule is adopted or rejected.

## 2026-05-12

- Reliability engineer reviewed the two triage-assistant proposals in [`learned.md`](/learned.md). The TK-101 level-oscillation observation was left **pending** (worth watching, not yet knowledge). The "M-201 current spikes predict P-101A trips" claim was **rejected**: both signals are driven by feed-rate changes, so the link is a shared cause, not prediction. Rejection reason recorded in full.

## 2026-05-10

- Triage assistant (`agent:triage-assistant`) proposed two observations into [`learned.md`](/learned.md): a possible TK-101 level oscillation following M-201 restarts, and a possible predictive link between M-201 current spikes and P-101A trips. Both recorded as agent-generated, awaiting human review.

## 2026-04-08

- Added the scoped process heuristic [`/heuristics/clarifier-settling-phase.md`](/heuristics/clarifier-settling-phase.md): low P-101A flow during the SETTLE phase is expected. Confirmed by the reliability engineer. Added [`/assets/slurry-feed-line-1.md`](/assets/slurry-feed-line-1.md) as the line-as-asset that declares the referenced `line_phase` stream, and published the [tag directory](/tag-directory.md).

## 2026-04-05

- Process engineering filed the [settling-phase note](/references/process-note-settling-phase.md): during SETTLE on CLARIFY-01 the feed is deliberately reduced, so low flow on P-101A in that phase is not a fault. Filed as ground truth for a scoped heuristic.

## 2026-03-20

- Trust policy adopted on [`/assets/slurry-charge-pump-101a.md`](/assets/slurry-charge-pump-101a.md): a reading not refreshed within the 30-minute window is treated as failed, conclusions from it are advisory-only, and no control action follows a stale reading. Sourced to Dana Reyes's email; verified by the reliability engineer.

## 2026-03-18

- Overnight near-miss: a frozen `TT-101A-BRG` bearing-temperature reading held its last value and nearly caused a healthy P-101A to be tripped. Dana Reyes's [email](/references/email-stale-transmitter-incident.md) filed, requesting a standing trust window.

## 2026-02-20

- Reliability review. The cold-start heuristic was reviewed and **confirmed** as [`/heuristics/pump-101a-cold-start.md`](/heuristics/pump-101a-cold-start.md), sourced to Joe Miller's handover note. The operator-observed M-201 → TK-101 lead/lag was documented in the [minutes](/references/reliability-review-minutes.md) and recorded as a `LEADS` edge in [`/relations.md`](/relations.md), explicitly as observation, not prediction.

## 2026-02-16

- Cold-start observation recorded as **pending** from the handover note, awaiting reliability review.

## 2026-02-14

- Joe Miller filed a [shift-handover note](/references/shift-handover-cold-start.md) describing the winter cold-start inlet-pressure dip on P-101A and the short wait that tells it apart from a real fault. First appearance of the cold-start knowledge.
