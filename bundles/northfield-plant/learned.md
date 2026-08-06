---
type: Reference
title: "Agent-proposed observations (learned)"
description: "The staging area for facts proposed by the triage assistant: one pending observation awaiting review, one claim rejected with the engineer's reason."
resource: /learned.md
tags: [learned, provenance, review-lifecycle, agent-proposed]
generated: { by: agent:triage-assistant, at: 2026-05-10T04:15:00Z }
status: draft
proposed_claims:
  - claim: "TK-101 level oscillation appears to follow M-201 restarts; proposing a monitoring note so an engineer can decide whether it is worth watching."
    contributor: agent:triage-assistant
    source: triage-obs-tk101-oscillation
    quote: "Across three M-201 restarts this week, a low-amplitude oscillation on TK-101 level was observed to begin shortly after each restart; proposing this as a monitoring note for human review."
    confidence: low
    review_status: pending
  - claim: "M-201 line-current spikes predict P-101A trips."
    contributor: agent:triage-assistant
    source: triage-obs-m201-current-p101a-trip
    quote: "In the sampled window, several M-201 line-current spikes preceded P-101A trips; proposing a predictive relationship for human review."
    confidence: low
    review_status: rejected
    rejection_reason: >
      Rejected by the reliability engineer. Both M-201 line current and P-101A trip
      conditions are driven by upstream feed-rate changes, so the apparent link is a
      shared cause, not prediction: the feed change moves both signals independently.
      Publishing this as a predictive edge would teach an agent to forecast a trip from
      a confounded correlation. If a genuine mechanism is ever established, it should be
      recorded as a sourced LEADS observation with a stated method — not as prediction.
    verified:
      - { by: human:rokafor, at: 2026-05-12T09:30:00Z }
sources:
  - id: triage-obs-tk101-oscillation
    resource: "monitoring://triage-assistant.northfield.example/observations/2026-05-10/tk101-level-oscillation"
    system: "Triage assistant observation log"
    title: "Triage assistant observation — TK-101 level oscillation after M-201 restarts"
  - id: triage-obs-m201-current-p101a-trip
    resource: "monitoring://triage-assistant.northfield.example/observations/2026-05-10/m201-current-p101a-trip"
    system: "Triage assistant observation log"
    title: "Triage assistant observation — M-201 current spikes and P-101A trips"
---

# Agent-proposed observations (learned)

This file is where the triage assistant proposes facts it thinks it has noticed. Nothing here is knowledge yet. A proposal becomes knowledge only when a human reviewer moves it into an asset, heuristic, or relation through a reviewed pull request. Agents propose here; agents never merge.

## Pending — TK-101 level oscillation after M-201 restarts

The assistant observed a low-amplitude oscillation on TK-101 level that seemed to begin shortly after M-201 restarts, and proposes recording a monitoring note.[^triage-obs-tk101-oscillation] Status is `pending`: an agent may mention this only as a hypothesis ("worth watching"), never act on it. It awaits a reliability engineer's review.

## Rejected — "M-201 current spikes predict P-101A trips"

The assistant proposed a predictive relationship after seeing M-201 line-current spikes precede P-101A trips in a sampled window.[^triage-obs-m201-current-p101a-trip] The reliability engineer **rejected** it (reviewed 12 May 2026). The reason is recorded in full above and is worth stating plainly: both signals are driven by upstream feed-rate changes, so this is a *shared cause*, not prediction — the feed change moves M-201 current and pushes P-101A toward a trip independently. A confounded correlation must not be published as a predictive edge. The rejection reason stays on the record so the same proposal is not re-raised, and so the cause-versus-confounder lesson is preserved.

[^triage-obs-tk101-oscillation]: Triage assistant observation — TK-101 level oscillation after M-201 restarts. `monitoring://triage-assistant.northfield.example/observations/2026-05-10/tk101-level-oscillation`
[^triage-obs-m201-current-p101a-trip]: Triage assistant observation — M-201 current spikes and P-101A trips. `monitoring://triage-assistant.northfield.example/observations/2026-05-10/m201-current-p101a-trip`
