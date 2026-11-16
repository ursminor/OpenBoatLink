<p><a href="../README.md"><img src="../brand/img/header.svg" alt="OBL OpenBoatLink" width="100%"></a></p>

[OpenBoatLink](../README.md) › [Specification](README.md) › Motivation and use cases

# Motivation and use cases

`v0.7` &nbsp; `2026-11-16` &nbsp; `CC BY 4.0` &nbsp; <img src="../brand/img/tag-draft.svg" alt="Draft" height="20" align="absmiddle">

> **In short.** Today every tracking, start or safety system brings its own radio, and the systems cannot work together. OBL is one open radio link for all of them. This page says why, and what OBL is used for on the water.

## Motivation

Advanced electronics can make regattas and training more attractive for sailors and spectators: live tracking and replay, electronic starts with on-board countdown and OCS detection, umpiring support, telemetry for coaching, and automated safety check-in. Most events do not use them yet. Where they are used, each application brings its own proprietary radio and platform, the systems cannot share data, and cost and effort limit them to a few top events.

OpenBoatLink (OBL) is one open, royalty-free radio protocol for all these applications. Devices from different manufacturers interoperate without prior coordination. OBL specifies the physical layer, medium access and a compact message set. It builds on techniques proven in aviation, mining and construction (see [System overview](03-system-overview.md)), adapted to the ranges, speeds and fleet sizes of sailing. Three performance tiers let simple, affordable devices serve club and national racing, while Olympic and world championship events get centimetre-level positions and accurate headings, precise enough to decide starts, finishes and mark roundings. The core of the specification is also published as an open-source C library. Its modules that decide compatibility and security are used unchanged in every product, which keeps devices interoperable and simplifies testing; the other modules are recommended.

World Sailing recognises such systems as Augmented Race Management Systems (ARMS) under Policy D12. OBL covers the ARMS functions with one radio link and adds an open protocol, so that recognised devices of different vendors can be used together at one event. Appendix E maps the Policy D12 requirements to this specification.

## Use cases

- **Tracking:** live positions of the fleet for race committee, media and spectators; replay after the race; long-distance races across lakes and along the coast (see LoRa tracking).
- **Race management**, as Augmented Race Management System (ARMS): start sequence with GNSS-synchronized timing; position of the starting line and distance to it on board; OCS detection and notification of the boats concerned; course changes and other signals; finish detection with automatic scoring.
- **Umpiring:** positions, headings and turn rates in real time to support on-water umpire decisions; overlaps when a boat reaches the zone of a mark; penalty and exoneration signals to the boats concerned.
- **AI umpiring:** automated rule checks (overlap, mark room, right of way) based on high-rate tracking data.
- **Safety check-in/check-out:** automated presence control before, during and after racing; distress signalling (capsize, man overboard); geofencing.
- **Coaching and telemetry:** wind, heel and trim, rig loads and other sensor data, live on the water and recorded for debriefing and performance analysis.
- **Race mark monitoring and management:** position, drift, wind data and battery state of anchored and robotic marks.
- **RTK correction broadcast:** GNSS correction data for centimetre-level positioning of competitor boats and marks, improving all ARMS position data: start and finish lines, OCS identification and mark roundings.

---

← [Contents](README.md) &nbsp;·&nbsp; [Requirements and performance tiers](02-requirements-and-tiers.md) →

Chapters named after "see" that are not listed in the [contents](README.md) are not published here yet.
