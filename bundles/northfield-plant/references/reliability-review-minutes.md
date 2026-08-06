---
type: Reference
title: "Reliability review minutes — M-201 recirculation and TK-101 level"
description: "Minutes recording the operator-observed lead/lag between M-201 recirculation changes and TK-101 level, and the decision to record it as an observation, not a prediction."
resource: /references/reliability-review-minutes.md
tags: [M-201, TK-101, lead-lag, relations]
generated: { by: human:rokafor, at: 2026-02-20T15:30:00Z }
status: stable
---

# Reliability review — minutes

**Date:** 20 Feb 2026
**Chair:** R. Okafor, Reliability Engineer

## Attendees

- R. Okafor — Reliability
- Joe Miller — Maintenance / Millwright
- Dana Reyes — Process Engineering

## Item 1 — Cold-start heuristic on P-101A

Reviewed Joe's handover note on the winter cold-start pressure dip. Agreed it matches what the crew has seen for years. Approved to record as a confirmed heuristic against P-101A, sourced to the handover note.

## Item 2 — M-201 recirculation and TK-101 level

Operators raised a pattern they all recognize. Recorded verbatim:

> Whenever we bump M-201 recirculation up or down, the level at TK-101 follows about 12 minutes later. We've all watched it happen on the trend, but nobody's put a mechanism to it.

Discussion: this is a genuine, repeatable lead/lag, so it is worth recording as a typed relationship. **But** we were explicit that this is an *observation*, not a control rule and not a prediction. We do not know the mechanism, and both signals ultimately track feed rate, so we are labeling it operator-observed with medium confidence. It should never be presented to an agent as "M-201 predicts TK-101."

**Action:** record an operator-observed `LEADS` edge from M-201 to TK-101, medium confidence, sourced to these minutes.

## Item 3 — Any other business

None.
