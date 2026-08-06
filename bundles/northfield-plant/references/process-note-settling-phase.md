---
type: Reference
title: "Process note — low flow on P-101A during the SETTLE phase is expected"
description: "Process engineer's note explaining that reduced P-101A flow during the settling phase of clarification is deliberate, and flow alarms in that phase are not faults."
resource: /references/process-note-settling-phase.md
tags: [P-101A, LINE-1, SETTLE, CLARIFY-01, settling-phase]
generated: { by: human:dreyes, at: 2026-04-05T11:05:00Z }
status: stable
---

# Process note — settling phase and P-101A flow

**Author:** Dana Reyes, Process Engineering
**Date:** 5 Apr 2026
**Re:** Recurring "low flow" concern on P-101A during clarification

I keep getting asked about low-flow indications on P-101A, so here it is in writing.

During the **SETTLE** phase of the clarification procedure (the batch system knows it as CLARIFY-01), we deliberately cut the slurry feed so the clarifier can do its job. Flow on P-101A is *supposed* to drop off in that window. Recorded for the record:

> During SETTLE on CLARIFY-01 we back the feed right down on purpose, so a low-flow indication on P-101A in that phase is expected behavior, not a fault. A flow alarm during SETTLE is telling you the phase is doing what it should — don't chase it as a pump problem.

Two things to keep straight:

1. **The phase is not ours to declare.** Whether the line is actually in SETTLE is the batch system's call. Read it from the phase indication; never assume it. Outside SETTLE, low flow on P-101A means what it usually means and should be looked at.
2. **Don't hard-code the feed numbers here.** The setpoints for the reduced feed live in the batch system and change with the recipe. This note is about *judgment* — how to read a low-flow indication during settling — not about values.

If flow is low and the line is *not* in SETTLE, that's a different conversation. Treat this note as scoped to the SETTLE phase only.

— Dana
