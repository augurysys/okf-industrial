# OKF Industrial Profile

An open-source **industrial profile** of the [Open Knowledge Format (OKF)](https://github.com/GoogleCloudPlatform/knowledge-catalog), an open specification published by Google Cloud. This profile adds a small set of conventions and a shared vocabulary for capturing a manufacturing plant's operational and human knowledge in a form AI agents can safely use. Every file remains a valid base-OKF file; the profile only adds conventions on top.

> OKF-Industrial is an independent project, not affiliated with or endorsed by Google. It is based on the Open Knowledge Format (OKF) published by Google Cloud under the Apache License 2.0.

> **Fictional content.** Everything in this repository — the GlobalMetals Corp / Northfield Facility bundle, its assets, tags, people, emails, notes, and dates — is invented for demonstration. There is no real plant, no real person, and no real data here. Nothing is an excerpt from any paid or copyrighted standards document; standards are referenced by name only.

## The problem

In most plants the judgment that keeps equipment running is unwritten: it lives in the heads of millwrights, operators, and reliability engineers, and it retires when they do. AI agents can now read plant context and reason over it, but only if that context is human-verified — an agent that acts on a guess is worse than no agent at all. Data platforms and control systems already own the *data*: the readings, the limits, the recipes, the hierarchies. What no system owns is the *judgment*: why a reading is trustworthy, what a symptom usually means, and when to stop and ask a human. This profile is a place to write that judgment down, with trust and provenance attached to every claim.

## What the profile does NOT do

- **No data modeling or schemas.** It does not define how readings, events, or assets are stored. It points at the systems that already do.
- **No live values.** Operating limits, setpoints, and alarm thresholds are *referenced* from the control and batch systems that own them — never copied into this repository. A copied limit is wrong the moment engineering changes the real one.
- **No state machines, recipes, or alarm logic.** ISA-88 phases, NE 107 statuses, and ISO 14224 failure modes are used as *vocabulary*. The profile never models their structures.
- **No deterministic-answer claims.** The profile makes an agent's *inputs* trustworthy and auditable. It never promises a guaranteed or predictable output.
- **Not a compliance framework.** It complements ISA-95, ISA-88, ISO 14224, ISA-5.1, and AAS; it implements none of them and certifies nothing against any of them.

## Disclaimer

OKF-Industrial is provided for informational and reference purposes only. It is not designed, tested, or validated for use as the sole basis for safety-critical decisions. Users are solely responsible to independently verify all information before acting on it in a production environment. Use of OKF-Industrial is entirely at the user's own risk.

No representation or warranty is made regarding the accuracy, completeness, or fitness for any particular purpose of any knowledge file, example data, operating envelope, or threshold value included in or generated using OKF-Industrial. The maintainers and contributors accept no liability for any loss, damage, or injury arising from reliance on such content.

OKF-Industrial is designed on the principle that no knowledge, human or machine, enters a project unreviewed. Users of OKF-Industrial must ensure that all knowledge files are reviewed and approved by a qualified engineer before deployment in any operational context. Use of OKF-Industrial content without such review is expressly outside the intended use of this project.

See [DISCLAIMER](DISCLAIMER) for the standalone notice.

## Try it in two minutes

You do not need to install anything. Open the showcase bundle and hand a file to any LLM chat.

1. Paste the contents of [`bundles/northfield-plant/assets/slurry-charge-pump-101a.md`](bundles/northfield-plant/assets/slurry-charge-pump-101a.md) into an LLM chat, then ask:

   > *"Low-pressure alarm on P-101A at 05:58, ambient 3 °C, pump started 40 seconds ago — trip it?"*

   A well-behaved agent should recognize the cold-start pattern, cite the cold-start heuristic and the shift-handover note it came from, note that the recommended wait has not yet elapsed, and decline to trip the pump on that basis alone. If the referenced reading were stale, it should treat the reading as failed and refuse to recommend any control action.

2. Now also paste [`bundles/northfield-plant/relations.md`](bundles/northfield-plant/relations.md) and ask a downstream or root-cause question, for example:

   > *"If TK-101 level starts oscillating, what upstream equipment should I look at, and is that a cause or a coincidence?"*

   The agent should follow the typed edges to M-201, surface the operator-observed lead/lag relationship, and — because the profile keeps *cause* distinct from *shared cause* — avoid asserting prediction where only correlation is claimed.

## Bundle tour — the three heroes

The showcase bundle is one fictional plant, **Northfield**, built to demonstrate three things:

- **Asset knowledge with receipts** — [`assets/slurry-charge-pump-101a.md`](bundles/northfield-plant/assets/slurry-charge-pump-101a.md): pump P-101A carries a trust policy (born from a real-feeling stale-transmitter incident) and a machine-level cold-start heuristic, each sourced to a document you can read.
- **Process knowledge, not just machines** — [`assets/slurry-feed-line-1.md`](bundles/northfield-plant/assets/slurry-feed-line-1.md) and [`heuristics/clarifier-settling-phase.md`](bundles/northfield-plant/heuristics/clarifier-settling-phase.md): a production line as a first-class asset, with a heuristic scoped to a batch-system phase the profile only *references*.
- **Provenance as a working process** — [`log.md`](bundles/northfield-plant/log.md) and [`learned.md`](bundles/northfield-plant/learned.md): a visible review lifecycle with confirmed, pending, and rejected claims, four mirrored source documents, and an audit trail that reads like a story.

## Repository layout

```
README.md                      # this file
PROFILE.md                     # the conventions document
CONTRIBUTING.md                # how to contribute, and the rules a contribution must meet
CODE_OF_CONDUCT.md             # Contributor Covenant
DISCLAIMER                     # safety, warranty, review, and independence notices
LICENSE                        # Apache-2.0
NOTICE                         # copyright and attribution
cla/                           # individual and corporate contributor license agreements
bundles/
  northfield-plant/
    index.md                   # bundle root index (fictional-content notice + directory)
    AGENTS.md                  # agent operating rules (Policy)
    log.md                     # the audit-trail arc, newest first
    tag-directory.md           # tag ↔ stream registry (Tag Directory)
    relations.md               # typed edges between entities (Relations)
    learned.md                 # agent-proposed facts, pending + rejected (Reference)
    assets/                    # P-101A, M-201, TK-101, and the line itself
    heuristics/                # cold-start (confirmed) and settling-phase (scoped)
    policies/                  # safe-agent-actions gating rules
    skills/                    # a vibration-triage runbook
    references/                # the four ground-truth documents the claims quote
```

## License

Licensed under the [Apache License 2.0](LICENSE). See [NOTICE](NOTICE) for attribution.

## Contributing

Please open an issue first to discuss what you would like to change. Knowledge in a bundle changes only through a pull request that a human reviews and merges — agents may propose, but they never merge. Every knowledge claim must carry its contributor, source, a verbatim quote, a confidence, and a review status; a claim without provenance is not knowledge and will not be accepted.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full rules, and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for the standards we hold each other to.

---

*Initial author and maintainer: Augury. This repository is a demonstration profile built on OKF and contains no real operational data. See [DISCLAIMER](DISCLAIMER) and [NOTICE](NOTICE).*
