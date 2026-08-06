---
type: Policy
title: "Safe agent actions — gating rules"
description: "Conditions that must hold before an agent recommends (never executes) an intervention; limits are referenced by identifier, never by value."
resource: /policies/safe-agent-actions.md
tags: [safety, policy, action-gating]
generated: { by: human:rokafor, at: 2026-03-20T09:20:00Z }
verified:
  - { by: human:rokafor, at: 2026-03-20T09:20:00Z }
status: stable
sources:
  - id: dcs-vib-trip-p101a
    resource: "opc.tcp://dcs.northfield.example/limits/P101A.VibHigh"
    standard: ISA-95
    system: DCS
    title: "P-101A high-vibration trip limit (value owned by the DCS)"
---

# Safe agent actions

An agent using this bundle **recommends**; it never **executes**. Control actions are taken by people and control systems, not by an agent. These are the gates that must hold before an agent recommends any intervention on Northfield equipment.

## Gates that must all hold before recommending an intervention

1. **Live inputs.** Every reading the recommendation depends on is live within its trust window. If any is stale, apply the [asset trust policy](/assets/slurry-charge-pump-101a.md): the conclusion is advisory-only and no control action may be recommended.
2. **Confirmed knowledge only.** The recommendation rests on `confirmed` claims. Pending claims may be mentioned as hypotheses; rejected claims are ignored.
3. **Expected-behavior check.** Rule out known expected patterns first — a [cold-start dip](/heuristics/pump-101a-cold-start.md) or [low flow during SETTLE](/heuristics/clarifier-settling-phase.md) — before treating a symptom as a fault.
4. **Limits belong to their owners.** Any comparison against a trip or alarm limit refers to the limit by its identifier only — for example the DCS-owned high-vibration trip limit for P-101A.[^dcs-vib-trip-p101a] The agent never states, guesses, or copies the limit value; it defers to the system that owns it.
5. **Human in the loop for control.** The output is a recommendation with its reasoning and citations. A human decides and acts.

## What an agent must not do

- Recommend a control action on stale or unconfirmed data.
- State a numeric limit, setpoint, or threshold. Those live in the control and batch systems; reference the identifier and stop there.
- Present a recommendation as a guaranteed or deterministic outcome.

[^dcs-vib-trip-p101a]: P-101A high-vibration trip limit, value owned by the DCS. `opc.tcp://dcs.northfield.example/limits/P101A.VibHigh`
