# Frequency is destiny: reading a drone from its control band

*RF engineering · field research note*

## The question

A commercial drone is, from a radio point of view, a talkative device. It listens for commands and sends video home. If you know which frequencies it uses, you already know a great deal about how it behaves and how it can be found. What does a control band actually tell you?

## What the public sources say

The JIATF-401 counter-drone reference guide lists the transceiver frequencies typically used by commercial off-the-shelf drones: **2.4 and 5.8 GHz, plus 433 MHz, 900 MHz and 1.2 GHz.** These are not arbitrary. They are the licence-free and lightly-licensed bands available cheaply worldwide, and each sits at a different point on one physical trade-off.

## The analysis

There is a single rule that governs radio, and it explains the whole list. **Lower frequencies travel further and pass through obstacles and weather more easily, but carry less information. Higher frequencies carry far more data and resolve finer detail, but fade faster and are stopped by walls and rain.**

Free-space path loss captures the distance-and-frequency part in one line:

```
FSPL (dB) = 20 log10(distance) + 20 log10(frequency) + 32.44
```

(distance in km, frequency in MHz). Loss grows with both terms, so a higher band costs you range for the same power. Read against the drone bands:

| Band | Character | What it is usually doing |
| --- | --- | --- |
| 433 / 900 MHz | Long reach, low data rate | Long-range control links, telemetry |
| 1.2 GHz | Middle ground | Control or analogue video on some models |
| 2.4 GHz | Balanced, congested | The default control link (shared with Wi-Fi) |
| 5.8 GHz | Short reach, high data rate | Video downlink, higher-bandwidth control |

So a drone screaming video on 5.8 GHz is close and bandwidth-hungry; a quiet 900 MHz telemetry beacon may be reaching much further. The band is a fingerprint of intent and range.

## Why it matters for detection

This is also the basis of **passive RF detection**: rather than radiating (as radar does), a passive sensor simply listens for these known control and video emissions and, with an antenna array, estimates the bearing to them. It is cheap, gives early warning, and never gives away its own position. Its blind spot is the one that keeps recurring in this field: the drone flying a pre-programmed route with its radio off has nothing to hear.

The one-line version: **when someone tells you a drone's frequency, they have told you most of its range, its data rate, and how you would find it.**

## Sources

- JIATF-401, *C-sUAS Quick Reference Guide*, V4, 2026 (cleared for open publication) for the commercial drone transceiver bands.
- Free-space path loss is standard radio engineering (Friis transmission, ITU-R references).
