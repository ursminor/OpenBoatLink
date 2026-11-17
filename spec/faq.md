<p><a href="../README.md"><img src="../brand/img/header.svg" alt="OBL OpenBoatLink" width="100%"></a></p>

[OpenBoatLink](../README.md) › [Specification](README.md) › FAQ

# FAQ

`v0.7` &nbsp; `2026-11-17` &nbsp; `CC BY 4.0` &nbsp; <img src="../brand/img/tag-draft.svg" alt="Draft" height="20" align="absmiddle">

> **In short.** Short answers to common questions: cost and hardware, licence, range, AIS or mobile network trackers, the racing rules, encryption, and the radio design (band, LoRa, TDMA, mesh).

## What does an OBL device cost?

It depends on the tier, mainly through the GNSS receiver and antenna. A standalone Tier 3 node starts at about USD 20 in parts, a Tier 2 node with a 10 Hz multi-constellation module at USD 25-35. A Tier 1 node needs an RTK receiver and a multi-band antenna, about USD 100-150 more at 2026 prices. Adding an OBL RF module to a device that already has GNSS costs about USD 10; see Hardware implementation and Appendix B.

## Can I use Meshtastic or other LoRa hardware?

Yes, for some nodes. Many boards sold with Meshtastic firmware have the right radio chip (Semtech SX1262) and a GNSS receiver. With OBL firmware instead of Meshtastic they work as relay nodes, receive-only gateway nodes, and as tier 3 boat nodes at events without authentication. A LoRaWAN gateway receives the OBL LoRa tracking packets with the software it is sold with, set to the OBL channels; only its output has to be converted. Appendix F lists suitable products; none has been tested with OBL yet. OBL and Meshtastic devices do not talk to each other: they share the radio chip, not the protocol.

## Do I need a radio licence or registration?

No. OBL uses bands for short-range devices that need no licence: 865-868 and 869.4-869.65 MHz in Europe, 902-928 MHz in the USA and Canada, 915-928 MHz in Australia and New Zealand (under a class licence, without an individual licence). Unlike AIS, a device needs no MMSI. It takes the region, and with it channels, power and airtime limits, from its GNSS position (see Channel plan). Channel plans for other regions are not defined yet. For an event, the entry names the addresses of the boat's devices, like the sail number (see Registration).

## What is the range?

It depends mostly on the height of the antennas: close to the water, the signal fades much faster with distance. Estimates for a portable device 0.3 m above the water, with a 10 dB safety margin, still to be confirmed on the water:

| Link | Radio mode | Range |
| --- | --- | --- |
| Boat to boat | HB | 150-380 m |
| Boat to committee boat (antenna 3 m) | HB | 0.6-1.1 km |
| Committee boat to boat | LR | 1.4-2.2 km |
| Boat to committee or gateway boat (antenna 3 m) | LoRa | 2.3-3.5 km |
| Committee boat (antenna 3 m) and mark (antenna 1 m), both ways | LoRa | 5-6 km |
| Boat to shore gateway (antenna 10 m) | LoRa | 4-6 km |
| Boat to gateway on a hill (300 m) | LoRa | 20-35 km |

Marks can lie 5 km or more from the committee boat. Beyond direct range, a LoRa relay forwards mark commands and their answers. A higher antenna on the boat, relay nodes and gateway boats also extend the other ranges (see Antenna and installation, Relaying, LoRa tracking).

## Why not AIS?

AIS is safety-of-navigation infrastructure on protected VHF channels. Its 9.6 kbit/s SOTDMA channels cannot carry 150 targets at racing update rates, transponders are expensive, and regulators do not allow sports traffic on the band. Boats that carry AIS keep it.

## Why not cellular or satellite trackers?

Cellular coverage on the water is often marginal and drops when spectators load the network. The modem dominates power consumption and cost, every device needs a subscription, and all data passes through a server, which adds latency. And there is no boat-to-boat path, which umpires, race committee and safety boats need. OBL gateways connect to the internet where coverage exists.

## Can OBL replace flags and hails under the racing rules?

Yes, if the sailing instructions change the rules concerned, as events using an Augmented Race Management System (ARMS) already do. Appendix D gives sailing instruction text.

## Is OBL encrypted?

Optionally. All critical data is authenticated: race management, RTK and, where the event requires it, tracking messages carry MACs that every receiver, including other boats, can verify (see Authentication). An event can also encrypt the tracking and telemetry of boats, so that boats cannot use each other's live data while racing. The race committee, umpires and authorized gateways read it live; the organizer publishes the keys after racing, so all data becomes public (see Encryption). Encryption also lets the organizer or a class control who distributes live tracking data. The no_track flag covers privacy outside competition.

## Why 868/915 MHz and not 2.4 GHz?

Sub-GHz signals propagate much better over water: lower path loss, better diffraction around waves and hulls, less absorption by spray and rain. The 2.4 GHz band is crowded with Wi-Fi and Bluetooth at regatta venues. Sub-GHz antennas are still small enough for buoys and dinghies.

## Why not LoRa for all traffic?

Airtime. A LoRa tracking packet takes 67 ms, an HB packet 0.8 ms, so 150 boats reporting every second do not fit, and frequent transmissions conflict with duty-cycle limits. GFSK at 300 kbit/s gives up range for about 80 times the capacity. LoRa is used where range counts more than rate: one packet per boat every 10 to 45 s, which also carries five recent track points, and commands to distant marks (see LoRa tracking).

## Why slotted random access, and not TDMA?

It is simple, needs no registration or slot assignment for competitors, degrades gracefully under overload and is easy to make interoperable. The slot grid, based on the GNSS timing every device has, roughly doubles the throughput compared to unslotted ALOHA, and the occupancy map avoids most remaining conflicts. Infrastructure that needs deterministic access (RTK, race management) has scheduled slots.

## Why no mesh?

With moving nodes a mesh cannot guarantee coverage, and it adds overhead and complexity. OBL uses medium-range links with an optional single relay hop. This extends coverage and keeps the protocol stateless and predictable.

---

← [System overview](03-system-overview.md) &nbsp;·&nbsp; [References](references.md) →

Chapters named after "see" that are not listed in the [contents](README.md) are not published here yet.
