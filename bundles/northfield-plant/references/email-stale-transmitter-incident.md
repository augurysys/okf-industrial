---
type: Reference
title: "Email — overnight phantom bearing alarm on P-101A (stale transmitter)"
description: "Process engineer's email after a frozen bearing-temperature reading nearly caused a healthy pump to be tripped; asks for a standing trust window."
resource: /references/email-stale-transmitter-incident.md
tags: [P-101A, TT-101A-BRG, stale-data, trust-policy]
generated: { by: human:dreyes, at: 2026-03-18T08:12:00Z }
status: stable
---

# Email

**From:** Dana Reyes, Process Engineering
**To:** Reliability; Control Room
**Cc:** R. Okafor
**Date:** 18 Mar 2026, 08:12
**Subject:** Near-miss overnight — we almost tripped a healthy P-101A on a frozen reading

All,

We had a near-miss on the night shift and I want us to fix the process, not just the sensor.

Around 02:00 the control room saw a bearing-temperature alarm on P-101A and started walking through the trip checklist. It turned out the bearing transmitter TT-101A-BRG had stopped reporting some time earlier and the display was simply holding its last value. The number on the screen looked like a live, alarming reading. On-call very nearly tripped a perfectly healthy pump on the strength of a reading that was hours old.

The uncomfortable part: nothing on the screen said the reading was stale. A frozen value and a live value look identical.

Here's what I'd like us to adopt as a standing rule:

> If a reading hasn't refreshed within the last 30 minutes, treat it as failed — not as data. Any conclusion that leans on it is advisory only. Do not take a control action off a stale reading; send someone to check the transmitter and the local gauge first.

Thirty minutes is a round number we can all remember and it's comfortably longer than the normal refresh interval, so a genuinely live sensor will never trip it. I'd rather we lose a little sensitivity than trip a healthy pump in the dark on a number that stopped moving.

Can reliability own writing this down against P-101A so the next on-call has it in front of them?

Thanks,
Dana
