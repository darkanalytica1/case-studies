# Attacking navigation: GNSS jamming versus spoofing

*Security · field research note*

## The question

Most small drones, and a great deal else, depend on satellite navigation. Those signals arrive at the ground extraordinarily weak, which makes them both easy to drown out and easy to imitate. Two attacks exploit this, and confusing them is a reliable sign that someone has not done the work. What is the difference, and how do you defend against each?

*Everything below is conceptual and defensive, at the level of publicly documented principles. It describes how these effects work and how to counter them, not how to build one, and applies only to systems you own or are authorised to test.*

## The two attacks

**Jamming is denial.** The attacker floods the receiver's band with noise until the real, faint satellite signals are lost beneath it. In signal terms, jamming collapses the signal-to-noise ratio to the point where the receiver can no longer lock on. The important consequence: **the drone knows it has lost navigation.** It can react, hold position, fall back to inertial or visual navigation, or return home.

**Spoofing is deception.** The attacker transmits counterfeit satellite signals, slightly stronger than the real ones, crafted so the receiver computes a false position and time. The important consequence: **the drone does not know it is wrong.** It flies confidently to the attacker's chosen coordinates. This is the more dangerous of the two, precisely because there is no obvious failure to react to.

| | Jamming | Spoofing |
| --- | --- | --- |
| Mechanism | Overpower with noise | Counterfeit the signal |
| Effect | Loss of lock (denial) | False position (deception) |
| Does the target know? | Yes | No, usually |
| Harder to detect? | No | Yes |

## Defending against both

The defences are layered, and none is a single silver bullet:

- **Do not depend on the signal.** Inertial navigation and vision-based navigation need no external radio, so a drone that can hold its course without satellites is far harder to deny or deceive. This is why "GPS-denied performance" is such a meaningful axis when comparing platforms.
- **Protect the antenna.** A controlled-reception-pattern antenna is an array that steers nulls toward the direction of interference, suppressing a jammer or spoofer while keeping the real satellites in view.
- **Sanity-check the fix.** A position that jumps, a time that drifts, or a signal that is suspiciously strong are all detectable tells of spoofing when the receiver is designed to look for them.
- **Cross-check.** Agreement between satellite, inertial and visual estimates is hard to fake across all three at once.

## Why it matters

The distinction is not academic. If your threat is jamming, resilience means graceful fallback: the system notices and copes. If your threat is spoofing, resilience means *detection and cross-checking*, because the system will otherwise be confidently, quietly wrong. Buying anti-jam protection and assuming you are also anti-spoof is a common and expensive mistake.

The one-line version: **jamming makes the drone lost; spoofing makes it lied to. Defend accordingly.**

## Sources

- Satellite-navigation vulnerability to interference and the jamming-versus-spoofing distinction are widely documented in public GNSS and resilient-PNT literature (for example US DHS and academic resilient-PNT material).
- Controlled-reception-pattern antennas and inertial / visual navigation are standard, publicly described mitigations.
