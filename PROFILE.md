# The OKF Industrial Profile

This document defines the conventions of the industrial profile. It is public documentation, not a build script: read it to understand how a bundle in this repository is shaped and why.

A **profile** is a disciplined way of using an existing open format. Every file in a bundle is a valid base-OKF (v0.2) file. The profile adds a type roster, a few frontmatter shapes, and a set of binding and provenance rules. A consumer that knows nothing about this profile can still parse and read every file, because all profile-specific keys are additive and ignorable.

## 1. What a bundle is

A bundle is a directory tree of Markdown files. Each concept file carries YAML frontmatter with a required `type` and, recommended, `title`, `description`, `resource`, and `tags`. Two files are reserved:

- `index.md` — a directory listing. Frontmatter is permitted only at the bundle root, and only the single key `okf_version: "0.2"`.
- `log.md` — a date-grouped history using `## YYYY-MM-DD` headings, newest first.

The profile targets **OKF v0.2**. It uses the v0.2 provenance and lifecycle keys and does not use any legacy v0.1 convention — there is no top-level `timestamp:` key and no `# Citations` body section anywhere.

## 2. Provenance and lifecycle keys

These keys are upstream OKF's; the profile only insists that industrial knowledge use them consistently.

- `generated: { by: <actor>, at: <ISO-8601> }` — who wrote the content. Actors are written `human:<id>` for people, or an agent/tool id such as `agent:triage-assistant`.
- `verified: [{ by: <actor>, at: <ISO-8601> }]` — who confirmed it. A `human:<id>` entry marks the human-reviewed trust tier.
- `sources: [ ... ]` — the materials a concept derives from and the external identifiers it defers to (see §4).
- `status: draft | stable | deprecated` — absent means `stable`.
- `stale_after: YYYY-MM-DD` — when the knowledge should be revisited.

## 3. Type roster

Use only these types, in Title Case:

| Type | Used for |
|---|---|
| `Asset` | A machine, vessel, or a production line treated as a first-class entity. |
| `Heuristic` | A single piece of operator or engineering judgment, with its receipt. |
| `Tag Directory` | The registry binding instrument tags to streams and owning assets. |
| `Relations` | Typed edges between entities. |
| `Reference` | A mirrored document — an email, a note, meeting minutes. |
| `Skill` | A runbook, with `When to use` / `Preconditions` / `Steps` / `Post-conditions`. |
| `Policy` | Agent operating rules and safety rules. |

A production line is an `Asset`. A static vessel is an `Asset`. Runbooks are `Skill`; agent and safety rules are `Policy`; the documents that claims quote are `Reference`.

## 4. Sources — one crosswalk mechanism

All external identifiers go through a single `sources[]` list. There are no custom per-standard blocks. Each entry carries derivation provenance (a document a claim came from) or an identifier crosswalk (an external-system identifier the knowledge defers to), or both. The only profile-conventional keys are `standard` and `system`, both optional.

```yaml
sources:
  - id: dcs-vib-trip-p101a
    resource: "opc.tcp://dcs.northfield.example/limits/P101A.VibHigh"
    standard: ISA-95
    system: DCS
    title: "P-101A high-vibration trip limit (value owned by the DCS)"
  - id: handover-cold-start
    resource: /references/shift-handover-cold-start.md
    title: "Shift handover note — cold-start pressure dip"
```

`id` is a stable key. Claims and markdown footnotes join to it by name, not by position.

## 5. Telemetry streams — pointers only

A stream is an endpoint pointer: a tag and a resource, nothing more.

```yaml
telemetry_streams:
  vibration:    { tag: VT-101A-DE,  resource: "opc.tcp://edge.northfield.example/P101A/vibration" }
  bearing_temp: { tag: TT-101A-BRG, resource: "historian://pi.northfield.example/P101A_BRG_TEMP" }
```

There is no `last_seen`, no `frozen`, and no current reading — liveness is a runtime question, checked live at decision time, never authored into a file. Tags follow ISA-5.1 conventions (first letter is the measured variable, following letters the function).

**Binding rule (both directions):** every stream `tag` must appear in the Tag Directory, and every tag in the Tag Directory must be bound to a declared stream.

## 6. Trust policy — the rule the profile owns

Most facts belong to some other system. The trust policy is one the profile genuinely owns, because no control system tells you how long to believe a reading:

```yaml
trust_policy:
  trust_window_minutes: 30
  when_stale: >
    Treat the reading as failed, not as data. Conclusions that depend on it are
    advisory-only. Never take a control action based on a stale reading; verify
    at the transmitter and the local gauge first.
  source: email-stale-transmitter
  verified: { by: human:rokafor, at: 2026-03-20T09:00:00Z }
```

The trust window is a policy parameter with no other owner, so it lives here — and it still carries a `source` receipt and a human `verified` record. NE 107 status names (Good, Maintenance-required, Out-of-spec, Failure) may be used as vocabulary when interpreting a device's referenced status; they are never authored as values.

## 7. The per-claim knowledge contract

Every knowledge claim — whether a `tribal_knowledge` entry on an asset or a standalone `Heuristic` file — carries all of:

- `claim` — the judgment, in one plain sentence.
- `contributor` — who holds this knowledge.
- `source` — a `sources[].id`. The claim's receipt.
- `quote` — the verbatim words from that source.
- `confidence` — `high | medium | low`.
- `review_status` — `confirmed | pending | rejected`.

Optional: `contributor_certification`, `applies_when`, and `canonical: /path.md` when a file summarizes a claim whose canonical home is elsewhere. Per-claim attribution in prose uses markdown footnotes whose labels match the `sources[].id`.

A claim missing any one of these is not knowledge and does not belong in a bundle.

## 8. Scoped knowledge — `applies_when`

Conditions bind to declared telemetry streams, never to modeled states:

```yaml
applies_when:
  phase: SETTLE
  phase_stream: line_phase
```

The phase's *identity* is crosswalked through `sources[]`; its *live value* belongs to the batch system and is read from the named stream at decision time. The bundle never lists the phases or models the procedure.

## 9. Relations — typed edges

A `Relations` file carries edges with `from` and `to` (bundle-absolute entity paths that must resolve) and a `type` from a small closed set:

- `FLOWS_TO` — material flow.
- `PART_OF` — composition.
- `LEADS` — a cause claim: A tends to precede B. `LEADS` edges should carry `lag_minutes`, `confidence`, `method` (e.g. `operator-observed`), and `source` (a `sources[].id`).
- `MEASURES_SAME_AS` — duplication: two tags observe the same physical quantity.

Cause (`LEADS`) is kept explicitly distinct from duplication (`MEASURES_SAME_AS`). An observed lead/lag is not a promise of prediction; it is a labeled, sourced observation with a stated method and confidence.

## 10. The review lifecycle and trust tiers

Knowledge moves through visible states:

- **pending** — proposed, often by an agent, not yet reviewed. An agent may mention it only as a hypothesis.
- **confirmed** — a human reviewer approved it (recorded in `verified`). This is the human-reviewed trust tier; an agent may act on it.
- **rejected** — a human reviewer declined it, with a substantive reason recorded. An agent ignores it, and the reason stays in the record so the same mistake is not re-proposed.

`log.md` tells the arc across dates — incident, proposal, review, adoption — newest first. Agents propose through pull requests; a human reviews and merges. Agents never merge.

## 11. The boundary — what the profile must not own

The bundle owns a fact only if no other system owns it. Operating limits, setpoints, alarm thresholds, machine and phase state, recipes, and equipment hierarchies are owned by control systems, batch systems, and registries. The bundle **references their identifiers and never states their values**. No engineered numeric value appears anywhere in a bundle — not in frontmatter, not in prose presented as authoritative. A copied limit drifts the instant engineering changes the real one.

The profile also never claims a deterministic or guaranteed AI result. It governs the source, not the answer: it makes an agent's inputs trustworthy and auditable. The output remains probabilistic.

## 12. Standards posture

Standards are dictionaries here, not schemas to implement. The profile **complements ISA-95, ISA-88, ISO 14224, ISA-5.1, and AAS; it implements none of them.** It borrows their vocabulary — ISA-5.1 tag conventions, ISO 14224 failure-mode names, ISA-88 procedure and phase identifiers, NAMUR NE 107 status names — and crosswalks their identifiers through `sources[]`. It never reproduces their tables or text, and it is not a compliance or certification framework for any of them.

The profile's own checks are called *profile checks* or *publisher lint*, to keep them clearly distinct from OKF conformance. Augury is the initial author and maintainer; the profile speaks for no other party.
