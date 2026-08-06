---
type: Asset
title: "Primary Clarifier Tank TK-101"
description: "Static vessel receiving slurry from P-101A; deliberately minimal, to show the profile is not limited to rotating equipment."
resource: /assets/clarifier-tank-101.md
tags: [TK-101, tank, vessel, Refining-Section-B]
generated: { by: human:rokafor, at: 2026-02-20T16:05:00Z }
status: stable
telemetry_streams:
  level: { tag: LT-101, resource: "historian://pi.northfield.example/TK101_LEVEL" }
---

# Primary Clarifier Tank TK-101

## Operational overview

TK-101 is the primary clarifier tank on Slurry Feed Line 1. It receives slurry delivered by P-101A and is where the settling step of clarification happens. It is a static vessel with a single monitored stream — level — declared above and resolving through the [Tag Directory](/tag-directory.md).

This file is intentionally minimal. A tank has less to say than a pump, and the profile should show that plainly: not every asset is rotating equipment with a rich failure story, and a bundle is not obliged to invent one. What matters here is the tank's place in the process — it is downstream of P-101A and its level is the quantity M-201 recirculation appears to lead.

## Related context

- Upstream pump: [`/assets/slurry-charge-pump-101a.md`](/assets/slurry-charge-pump-101a.md)
- Line context: [`/assets/slurry-feed-line-1.md`](/assets/slurry-feed-line-1.md)
- Relationships (flow in, observed lead from M-201): [`/relations.md`](/relations.md)
