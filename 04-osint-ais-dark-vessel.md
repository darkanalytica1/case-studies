# Finding the ship running dark: fusing AIS with other open signals

*OSINT / maritime · field research note*

## The question

The sea is more transparent than it looks. Most large vessels continuously broadcast their identity and position over the Automatic Identification System, and that broadcast is public. The interesting vessel is usually not the one you can see on the map. It is the one that has just disappeared from it. How do you find the ship running dark using only open sources?

## What AIS is, and is not

AIS is a maritime safety system: ships transmit a standard message with an identity (the MMSI), position, course and speed, so others can avoid collisions. Coastal receivers and satellites pick these up, and several public and commercial services aggregate them into live maps. Two facts make it useful for open-source analysis:

- It is **cooperative**. A vessel that wants to be seen is seen.
- It can be **switched off, or falsified**. A vessel that turns its transponder off, or broadcasts a false identity or position, is doing something a compliant vessel does not do.

So AIS on its own tells you about the law-abiding traffic. The analytical value comes from the gaps and the contradictions.

## The method

The technique is fusion: treat the AIS picture as one layer and correlate it with other open layers to find what the AIS layer is hiding.

1. **Establish the baseline.** Normal traffic, normal routes, normal behaviour for the area and season. Anomalies only mean something against a baseline.
2. **Watch for the drop-out.** A vessel whose AIS goes dark in open water, especially near a sensitive area or at a sensitive time, is the signal. Note the last known position, course and speed; that defines a search box that grows predictably with time.
3. **Cross-check against non-cooperative layers.** Publicly available optical and radar satellite imagery, and wide-area optical search products, can reveal a vessel that is not transmitting. A radar or optical return with no matching AIS track is exactly the contradiction worth investigating.
4. **Check for identity spoofing.** Two vessels broadcasting the same identity, or a track that teleports or moves impossibly fast, are signs of falsified AIS rather than a genuine vessel.
5. **Build pattern of life.** Over time, repeated dark periods, rendezvous points and route deviations form a pattern that a single snapshot never shows.

## Why it matters

For a region like the Black Sea, maritime domain awareness built from open sources is genuinely valuable and genuinely public. A vessel going dark is not proof of wrongdoing, plenty of dark periods are innocent, but it is a lead, and the discipline of fusing a cooperative layer (AIS) with non-cooperative layers (imagery, radar) is the same discipline that runs through all of counter-drone and intelligence work: no single sensor is enough, and the interesting object is the one that does not agree with itself.

The one-line version: **on the sea, the signal is often the silence. AIS finds the honest traffic; fusion finds the rest.**

## Sources

- AIS is defined by the International Maritime Organization and ITU-R M.1371; vessel positions are published by multiple open aggregators.
- "Going dark" and AIS spoofing as maritime-awareness indicators are widely documented in open maritime-security and OSINT literature.
- Wide-area optical search and satellite imagery as non-cooperative cross-checks are publicly described techniques.
