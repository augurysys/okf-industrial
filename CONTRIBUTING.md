# Contributing

Thanks for your interest in the OKF Industrial Profile.

This repository holds a set of conventions layered on the Open Knowledge Format (OKF), an open specification published by Google Cloud, plus one worked example bundle. Contributions are welcome, whether that is a correction, a clearer explanation, a new convention proposal, or an additional example.

## Start with an issue

Please open an issue before sending a pull request, especially for anything that changes a convention. It saves you work: a convention change affects every bundle that follows this profile, so it deserves discussion first. Small fixes such as typos, broken links, or clarifications can go straight to a pull request.

## Ground rules for any contribution

These are not style preferences. They are the reason the profile is safe to use, and we will ask for changes to any pull request that breaks one.

1. **All example content must be fictional.** No real company, plant, site, person, tag, document, or reading. The example bundle uses an invented world (GlobalMetals Corp, the Northfield Facility) and any new example must do the same.
2. **No real operational data, ever.** Do not contribute anything taken from a live plant, historian, control system, or maintenance record, including anonymized extracts.
3. **Link, do not copy.** Operating limits, setpoints, alarm thresholds, machine and phase state, recipes, and equipment hierarchies belong to the systems that own them. Reference their identifiers through `sources[]`. Do not state their values. A copied limit is wrong the moment engineering changes the real one.
4. **No excerpts from paid standards.** Reference ISO, ISA, or NAMUR documents by name and number, and link to the publisher. Do not reproduce their tables, thresholds, or text.
5. **Provenance is required.** Every knowledge claim carries a contributor, a source, a verbatim quote, a confidence, and a review status. A claim without provenance is not knowledge and will not be merged.
6. **Humans merge, agents propose.** An agent may open a pull request or add a proposal to `learned.md`, but a human reviewer decides what becomes knowledge. Nothing merges itself.

## Before you open a pull request

Check your change against the profile's own rules, which are documented in [PROFILE.md](PROFILE.md):

- Every file still parses as a valid OKF file with a non-empty `type`.
- Types come from the profile's roster, in Title Case.
- Every tag in the tag directory binds to a declared stream, and every declared stream tag appears in the tag directory.
- Every `source` on a claim, and every footnote label, resolves to an entry in that file's `sources[]`.
- Every bundle-absolute link and path resolves to a real file.
- No engineered numeric value appears anywhere, in frontmatter or in prose presented as authoritative.
- No liveness values (`last_seen`, `frozen`, current readings). Liveness is checked at the endpoint at decision time.

These are the profile's own checks, not OKF conformance. OKF itself asks very little of a bundle, and consumers of OKF are expected to tolerate unknown fields and broken links rather than reject a bundle. The checks above are the stricter bar this repository holds its own content to.

## Contributor License Agreement

This project is licensed under the [Apache License 2.0](LICENSE). Before a contribution can be merged, we must have a signed Contributor License Agreement (CLA) on file from the contributor. The CLA gives an explicit copyright and patent license, confirms that the contributor has the authority to make that grant, and records that no confidential or third-party intellectual property was included.

Signing the CLA does not change your rights to use your own contribution for any other purpose. Except for the license granted to Augury and to recipients of software distributed by Augury, you keep all right, title, and interest in your contribution.

There are two agreements. Sign the one that applies to you:

- **[Individual Contributor License Agreement](cla/individual-cla.md)** — for a person contributing in their personal capacity.
- **[Corporate Contributor License Agreement](cla/corporate-cla.md)** — for a corporation or other legal entity authorizing contributions by its designated employees.

If your employer has rights to intellectual property that you create, you need either your employer's permission to contribute, a waiver from them, or a Corporate CLA signed by them.

Complete and sign the applicable agreement, then email a signed PDF copy to legal@augury.com.

## Code of conduct

Participation in this project is governed by our [Code of Conduct](CODE_OF_CONDUCT.md).
