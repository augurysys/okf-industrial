---
type: Relations
title: "Northfield relations"
description: "Typed edges between Northfield entities: material flow, composition, and one operator-observed lead/lag."
resource: /relations.md
tags: [relations, topology, lead-lag]
generated: { by: human:rokafor, at: 2026-02-20T16:10:00Z }
status: stable
edges:
  - from: /assets/slurry-charge-pump-101a.md
    to: /assets/clarifier-tank-101.md
    type: FLOWS_TO
  - from: /assets/slurry-charge-pump-101a.md
    to: /assets/slurry-feed-line-1.md
    type: PART_OF
  - from: /assets/clarifier-feed-motor-201.md
    to: /assets/slurry-feed-line-1.md
    type: PART_OF
  - from: /assets/clarifier-tank-101.md
    to: /assets/slurry-feed-line-1.md
    type: PART_OF
  - from: /assets/clarifier-feed-motor-201.md
    to: /assets/clarifier-tank-101.md
    type: LEADS
    lag_minutes: 12
    confidence: medium
    method: operator-observed
    source: reliability-review-minutes
sources:
  - id: reliability-review-minutes
    resource: /references/reliability-review-minutes.md
    title: "Reliability review minutes — M-201 / TK-101 lead-lag"
---

# Northfield relations

Typed edges between entities in this bundle. Every endpoint is a bundle-absolute path that resolves to a real file. Edge types are drawn from a small closed set: `FLOWS_TO` (material flow), `PART_OF` (composition), `LEADS` (a cause claim), and `MEASURES_SAME_AS` (duplication).

## Composition and flow

- P-101A **FLOWS_TO** TK-101 — the charge pump delivers slurry into the primary clarifier tank.
- P-101A, M-201, and TK-101 are each **PART_OF** Slurry Feed Line 1.

## The one cause claim, kept honest

- M-201 **LEADS** TK-101 — when M-201 recirculation changes, TK-101 level tends to follow about 12 minutes later. This is `operator-observed`, `medium` confidence, sourced to the reliability review minutes.[^reliability-review-minutes]

This is deliberately a `LEADS` edge and not a `MEASURES_SAME_AS` edge, and it is deliberately not sold as prediction. The lag is a labeled observation with a stated method and confidence, not a mechanism. Both signals ultimately track feed rate, so the relationship is best read as a shared cause, not as M-201 driving TK-101. An agent should use it to decide *where to look* when TK-101 level moves — never to forecast TK-101 from M-201. Keeping cause distinct from duplication, and observation distinct from prediction, is the whole point of typing these edges.

[^reliability-review-minutes]: Reliability review minutes — M-201 / TK-101 lead-lag. `/references/reliability-review-minutes.md`
