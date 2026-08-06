---
type: Tag Directory
title: "Northfield tag directory"
description: "The registry binding every instrument tag to the asset and declared stream it belongs to; the single place an agent resolves a tag."
resource: /tag-directory.md
tags: [tags, ISA-5.1, registry]
generated: { by: human:rokafor, at: 2026-04-08T10:20:00Z }
status: stable
entries:
  - tag: VT-101A-DE
    asset: /assets/slurry-charge-pump-101a.md
    stream: vibration
    resource: "opc.tcp://edge.northfield.example/P101A/vibration"
  - tag: TT-101A-BRG
    asset: /assets/slurry-charge-pump-101a.md
    stream: bearing_temp
    resource: "historian://pi.northfield.example/P101A_BRG_TEMP"
  - tag: FT-101A
    asset: /assets/slurry-charge-pump-101a.md
    stream: flow
    resource: "historian://pi.northfield.example/P101A_FLOW"
  - tag: PT-101A-IN
    asset: /assets/slurry-charge-pump-101a.md
    stream: inlet_pressure
    resource: "opc.tcp://edge.northfield.example/P101A/inlet_pressure"
  - tag: VT-201-NDE
    asset: /assets/clarifier-feed-motor-201.md
    stream: vibration_nde
    resource: "opc.tcp://edge.northfield.example/M201/vibration_nde"
  - tag: TT-201-STA
    asset: /assets/clarifier-feed-motor-201.md
    stream: stator_temp
    resource: "historian://pi.northfield.example/M201_STATOR_TEMP"
  - tag: IT-201
    asset: /assets/clarifier-feed-motor-201.md
    stream: line_current
    resource: "historian://pi.northfield.example/M201_LINE_CURRENT"
  - tag: LT-101
    asset: /assets/clarifier-tank-101.md
    stream: level
    resource: "historian://pi.northfield.example/TK101_LEVEL"
  - tag: YC-101-PHASE
    asset: /assets/slurry-feed-line-1.md
    stream: line_phase
    resource: "opc.tcp://edge.northfield.example/LINE1/phase"
---

# Northfield tag directory

Every instrument tag used anywhere in this bundle resolves here to exactly one asset and one declared stream. Agents must not guess a tag; resolve it here. Tags follow ISA-5.1 conventions — the first letter is the measured variable, the following letters the function. The directory is a pointer registry: it names endpoints, never live values.

The binding is two-way. Every tag declared as a stream on an asset appears in this table, and every tag in this table is bound to a stream declared on the named asset. A tag in one place but not the other is a lint error.

| Tag | Asset | Stream (logical) | Endpoint |
|---|---|---|---|
| `VT-101A-DE` | [P-101A](/assets/slurry-charge-pump-101a.md) | vibration | `opc.tcp://edge.northfield.example/P101A/vibration` |
| `TT-101A-BRG` | [P-101A](/assets/slurry-charge-pump-101a.md) | bearing_temp | `historian://pi.northfield.example/P101A_BRG_TEMP` |
| `FT-101A` | [P-101A](/assets/slurry-charge-pump-101a.md) | flow | `historian://pi.northfield.example/P101A_FLOW` |
| `PT-101A-IN` | [P-101A](/assets/slurry-charge-pump-101a.md) | inlet_pressure | `opc.tcp://edge.northfield.example/P101A/inlet_pressure` |
| `VT-201-NDE` | [M-201](/assets/clarifier-feed-motor-201.md) | vibration_nde | `opc.tcp://edge.northfield.example/M201/vibration_nde` |
| `TT-201-STA` | [M-201](/assets/clarifier-feed-motor-201.md) | stator_temp | `historian://pi.northfield.example/M201_STATOR_TEMP` |
| `IT-201` | [M-201](/assets/clarifier-feed-motor-201.md) | line_current | `historian://pi.northfield.example/M201_LINE_CURRENT` |
| `LT-101` | [TK-101](/assets/clarifier-tank-101.md) | level | `historian://pi.northfield.example/TK101_LEVEL` |
| `YC-101-PHASE` | [LINE-1](/assets/slurry-feed-line-1.md) | line_phase | `opc.tcp://edge.northfield.example/LINE1/phase` |
