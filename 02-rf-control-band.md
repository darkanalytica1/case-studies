# Frequency is destiny: reading a drone from its control band

*RF engineering · field research note 02*

## The question

A commercial drone is, from a radio point of view, a talkative device. It listens for commands and sends video home. If you know which frequencies it uses, you already know a great deal about how it behaves and how it can be found. What does a control band actually tell you?

## What the public sources say

The JIATF-401 counter-drone reference guide lists the transceiver frequencies typically used by commercial off-the-shelf drones: **2.4 and 5.8 GHz, plus 433 MHz, 900 MHz and 1.2 GHz.** These are not arbitrary. 2.4 GHz (2400 to 2483.5 MHz) and 5.8 GHz (5725 to 5875 MHz) are industrial, scientific and medical (ISM) bands usable licence-free almost everywhere. 433 MHz (433.05 to 434.79 MHz) is licence-free for short-range devices in ITU Region 1, which includes Europe; 902 to 928 MHz is the licence-free band in the Americas, with 868 MHz as the nearest European equivalent. 1.2 to 1.3 GHz is mostly an amateur or licensed band, used by some long-range analogue video links. Each band sits at a different point on one physical trade-off.

## The analysis

Two rules explain the list. **Lower frequencies reach further for the same antennas and power, and pass through foliage, walls and weather more easily. Higher bands offer wider channels, so they carry more data, but fade faster and are stopped by obstacles.** (The data rate follows from the channel bandwidth the band allows, not from the frequency itself; in practice the higher bands are where wide channels are available.)

Free-space path loss captures the distance-and-frequency part in one line:

```
FSPL (dB) = 20 log10(distance) + 20 log10(frequency) + 32.44
```

(distance in km, frequency in MHz, isotropic antennas). Loss grows with both terms: doubling the frequency adds about 6 dB, so a higher band costs you range for the same power and antenna gain. Read against the drone bands:

| Band | Character | What it is usually doing |
| --- | --- | --- |
| 433 / 868 / 900 MHz | Long reach, low data rate | Long-range control links, telemetry |
| 1.2 to 1.3 GHz | Middle ground | Analogue video or control on some long-range builds |
| 2.4 GHz | Balanced, congested | The default control link (shared with Wi-Fi) |
| 5.8 GHz | Shorter reach, high data rate | Video downlink, higher-bandwidth control |

Many current consumer links switch between 2.4 and 5.8 GHz automatically, depending on interference. So a drone streaming video on 5.8 GHz is likely bandwidth-hungry and operating within shorter reach, while a quiet 900 MHz telemetry link may be reaching much further. The band is a strong hint about range and data rate, not proof.

## Why it matters for detection

This is also the basis of **passive RF detection**: rather than radiating (as radar does), a passive sensor listens for known control and video emissions and, with an antenna array, estimates the bearing to them. It is comparatively cheap, can give early warning, and does not reveal its own position by transmitting. Its blind spot is the one that keeps recurring in this field: the drone flying a pre-programmed route with its radio off has nothing to hear.

The one-line version: **when someone tells you a drone's frequency, they have told you much of its likely range, its data rate, and how you would find it.**

## Limitations

Free-space loss ignores terrain, multipath and body or foliage loss, which also grow with frequency. Band allocations differ by country; check the national frequency table before relying on any band note above.

## Sources

- JIATF-401, *C-sUAS Quick Reference Guide*, V4, 2026 (cleared for open publication) for the commercial drone transceiver bands.
- ITU Radio Regulations (ISM bands, footnotes 5.138 and 5.150); CEPT ERC Recommendation 70-03 for European short-range device bands.
- Free-space path loss is standard radio engineering (Friis transmission equation; ITU-R P.525).
