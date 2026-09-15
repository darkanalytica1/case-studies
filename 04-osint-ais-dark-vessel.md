# Finding the ship running dark: fusing AIS with other open signals

*OSINT / maritime · field research note 04*

## The question

The sea is more transparent than it looks. Most large vessels continuously broadcast their identity and position over the Automatic Identification System, and that broadcast can be received by anyone. The interesting vessel is usually not the one you can see on the map. It is the one that has just disappeared from it. How do you find the ship running dark using only open sources?

## What AIS is, and is not

AIS is a maritime safety system: ships transmit standard messages with an identity (the MMSI), position, course and speed, so others can avoid collisions. Under SOLAS Chapter V, Regulation 19, AIS is required on ships of 300 gross tonnage and upwards on international voyages, cargo ships of 500 gross tonnage and upwards not on international voyages, and all passenger ships. Coastal receivers and satellites pick these messages up, and several public and commercial services aggregate them into live maps. Two facts make it useful for open-source analysis:

- It is **cooperative**. A vessel that wants to be seen is seen.
- It can be **switched off, or falsified**. SOLAS guidance allows the master to switch AIS off where its operation compromises safety or security (for example under piracy threat), so a dark period can be lawful. Outside those cases, a vessel that turns its transponder off, or broadcasts a false identity or position, is doing something a compliant vessel does not do.

So AIS on its own tells you about the cooperative traffic. The analytical value comes from the gaps and the contradictions.

## The method

The technique is fusion: treat the AIS picture as one layer and correlate it with other open layers to find what the AIS layer is hiding.

<p align="center">
  <img src="assets/diagrams/ais-dark-gap.svg" alt="An AIS track stops at a last fix; the possible area grows with time; a radar or optical return with no matching AIS inside it is the lead" width="900">
</p>

1. **Establish the baseline.** Normal traffic, normal routes, normal behaviour for the area and season. Anomalies only mean something against a baseline.
2. **Watch for the drop-out.** A vessel whose AIS goes dark in open water, especially near a sensitive area or at a sensitive time, is the signal. Note the last known position, course and speed.
3. **Bound the gap.** The area the vessel can have reached grows predictably with time: roughly a circle whose radius is its plausible maximum speed multiplied by the time since the last fix.
4. **Cross-check against non-cooperative layers.** Publicly available radar satellite imagery (for example Copernicus Sentinel-1 synthetic aperture radar) and optical imagery can reveal a vessel that is not transmitting. A radar or optical return with no matching AIS track is exactly the contradiction worth investigating.
5. **Check for identity spoofing.** Two vessels broadcasting the same MMSI, or a track that teleports or moves impossibly fast, are signs of falsified AIS rather than a genuine vessel.
6. **Build pattern of life.** Over time, repeated dark periods, rendezvous points and route deviations form a pattern that a single snapshot never shows.

## Why it matters

For a region like the Black Sea, maritime domain awareness built from open sources is genuinely valuable and genuinely public. A vessel going dark is not proof of wrongdoing, plenty of dark periods are innocent, but it is a lead. The discipline of fusing a cooperative layer (AIS) with non-cooperative layers (imagery, radar) is the same discipline that runs through all of counter-drone and intelligence work: no single sensor is enough, and the interesting object is the one that does not agree with itself.

The one-line version: **on the sea, the signal is often the silence. AIS finds the cooperative traffic; fusion finds the rest.**

## Limitations

Many AIS gaps are reception artefacts: terrestrial receivers have limited range, satellite AIS revisits intermittently and suffers message collisions in dense traffic. Satellite imagery is periodic, so a return may not exist for the time window you need. The figure uses illustrative geometry, not a real vessel.

## Sources

- AIS carriage requirements: International Maritime Organization, SOLAS Chapter V, Regulation 19, and IMO Resolution A.1106(29) guidelines for onboard operational use of AIS.
- AIS technical characteristics: ITU-R Recommendation M.1371.
- Copernicus Sentinel-1 mission documentation (European Space Agency) for openly available SAR imagery.
- "Going dark" and AIS spoofing as maritime-awareness indicators are widely documented in open maritime-security and OSINT literature.
