<p><a href="../README.md"><img src="../brand/img/header.svg" alt="OBL OpenBoatLink" width="100%"></a></p>

[OpenBoatLink](../README.md) › [Specification](README.md) › Requirements and performance tiers

# Requirements and performance tiers

`v0.7` &nbsp; `2026-11-16` &nbsp; `CC BY 4.0` &nbsp; <img src="../brand/img/tag-draft.svg" alt="Draft" height="20" align="absmiddle">

> **In short.** The first part lists what OBL must deliver: full performance for up to 150 boats, no set-up on the boat, low cost, an open specification. The second part describes the three device tiers: tier 3 for club racing, tier 2 for championships, tier 1 with centimetre accuracy for Olympic events. The notice of race or the sailing instructions state which tier an event needs.

## Requirements

- **Scale:** full performance for up to 150 boats within radio range; graceful degradation up to 600 boats; no collapse beyond.
- **Direct reception, low latency:** boats, umpires, coaches and race committee receive each other directly, within a second and without shore or internet infrastructure.
- **Licence-free operation:** sub-GHz ISM/SRD bands (868 MHz in Europe, 915/921 MHz in the Americas and Oceania) within regional power and access rules.
- **Scalable performance:** three performance tiers, from simple devices for club racing to RTK devices for Olympic events, all on the same protocol (see [OBL performance tiers](#obl-performance-tiers)).
- **Cost and power:** complete electronics of a standalone device USD 20-30 in bill of materials; less than USD 10 to add OBL to a device that already has GNSS. Several race days on a small battery or solar power.
- **Zero configuration:** boat devices are not configured for a regatta or a course. The only exception is a semi-permanent boat class setting.
- **Common hardware:** every component is a common part, available from at least two manufacturers.
- **Certification:** products built on a reference radio module need no radio tests of their own (see Radio certification).
- **Portable devices:** full function with an internal antenna of at most 100 mm, placed only 0.3 m above the water surface.
- **Robustness:** reliable over-water links between boats and infrastructure across a course of several kilometres.
- **Authenticity:** every receiver can verify sender, integrity and freshness of race management, correction and tracking data, without shared secrets or shore infrastructure. An event can encrypt boat data (see Encryption).
- **Openness:** public, royalty-free specification. Anyone may build receivers, and transmitters with an assigned address block.
- **Reference library:** the modules of the official C library that decide compatibility and security are mandatory and used unchanged in every product; the remaining modules are recommended (see Conformance disclosure).

## OBL performance tiers

OBL defines three performance tiers for devices, from tier 1 (highest) to tier 3 (lowest), like the grading of events. Tier 3 allows simple, affordable devices for club racing and training; tiers 2 and 1 serve championships and Olympic events. All tiers use the same protocol and share the same channels. A tier describes how well a device measures its position and how its data may be used, not how it communicates.

| Tier | Suggested events | GNSS, accuracy and fix rate | Heading | Authentication and encryption | ARMS use |
|---|---|---|---|---|---|
| 1 | Olympic Games, high-speed events | Centimetre level: RTK with the venue correction stream; fix rate at least 10 Hz | Required, within 2° (draft) | Required | Category 2 for all decisions |
| 2 | World and continental championships, international regattas, national championships | About 1 m: multi-constellation, single- or multi-band; accuracy reported with every fix; fix rate at least 10 Hz | Required, within 5° (draft) | Required | Category 2 for timing and OCS; a result can be too close to call |
| 3 | Club racing, training | Any GNSS; fix rate at least 1 Hz | Optional | None; no key store | Tracking; Category 1 |

The suggested events are guidance only; the notice of race or the sailing instructions state the minimum tier. A device meets a tier if it meets all requirements of that tier. It declares its tier in its information message (part 0), so that the race committee can check the fleet over the air.

Tier 1 and 2 devices shall measure the heading, normally with a magnetometer and IMU. Dual-antenna GNSS is an option where two antennas can be placed 20 cm or more apart, for example on yachts or on dinghies one at the stern and one in the display unit near the mast. OCS and zone calls place bow and stern from antenna position and heading; at low speed or in current, the course over ground does not show where the boat points. The heading limits in the table are provisional; they will be set with the manufacturers of heading units after trials on the water. They apply to the validity check described under Flags (hdg_valid). Each device reports its current accuracy in its tracking messages (pos_acc). The fix rate is the GNSS fix rate. Each device checks every fix against the prediction, so a higher fix rate detects manoeuvres sooner; tier 1 and 2 devices also record every fix on board (see On-board recording). The rate of transmitted reports follows from extrapolation-based reporting and the operating points (see Capacity and scaling).

Tier 3 devices need no key store. They do not authenticate or encrypt their own messages, but still verify authenticated infrastructure messages in software. Tier 1 and 2 devices authenticate their messages and encrypt them when the event requires it (see Authentication and Encryption). World Sailing ARMS Category 2 (rule-determining) depends on the decision. Timing decisions, such as the official start time, depend only on GNSS time and authenticated race committee messages. Position-based decisions, such as OCS identification, use the start report of the boat: it gives the margin to the line and the accuracy of the position, so the result is on the course side, not on the course side, or too close to call; the last group is decided by the race officer or the race officer's software, and every boat receives its status (see Racing procedures). Tier 1 and 2 devices are suitable for both. Tier 3 devices do not authenticate and are suitable for Category 1 (decision support) only.

Each tier also requires a minimum conformance: the following subtopics shall have the status Library or Complete in the device's Implementation Conformance Statement (see Conformance disclosure).

| Tier | Minimum conformance (ICS: Library or Complete) |
|---|---|
| 1 | All subtopics, including RTK |
| 2 | All subtopics, except RTK and optional telemetry subtypes |
| 3 | Shared-channel subtopics (Modulation and modes, Channel plan, Timing, Medium access control), LoRa tracking, tracking and information messages |

At every tier, the mandatory library modules shall be used unchanged (see Conformance disclosure). A device shall declare a tier in its information message only if its published ICS supports that tier. Once test vectors and conformance tests are published, a tier counts only for devices that have passed them.

---

← [Motivation and use cases](01-motivation-and-use-cases.md) &nbsp;·&nbsp; [System overview](03-system-overview.md) →

Chapters named after "see" that are not listed in the [contents](README.md) are not published here yet.
