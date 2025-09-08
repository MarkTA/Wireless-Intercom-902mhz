# Bill of Materials — Wireless Intercom (902–928 MHz, Full-Duplex Starter BOM)

This BOM is staged so you can prototype quickly and then tighten selectivity for full-duplex:
- **Stage A – Bench / Breadboard preselector (connectorized)**: in-line/cavity filters that protect your front-end from out-of-band energy while you bring up TX/RX.
- **Stage B – SMD ISM preselector (wide)**: board-level SAW/LTCC filters that pass the whole 902–928 MHz band (good OOB rejection, not channel-selective).
- **Stage C – Channel-select filters (narrower)**: options centered near ~906 MHz and ~920 MHz to improve TX↔RX isolation for simultaneous talk/listen.

> Notes:
> - For full-duplex, plan for **two distinct RF paths** (TX@920, RX@906) with appropriate filtering and isolation (directional coupler / hybrid) plus physical separation on the PCB.
> - Some channel-specific SAWs are specialty/industrial parts; availability varies. Keep Stage A/B handy during bring-up.

---

## RF front end

| Ref | Qty | Part / Option | Description & Key Specs | Use / Why it’s here | Package / Interface |
|---|---:|---|---|---|---|
| ANT1 | 2 | 915 MHz ISM whip + SMA | 902–928 MHz antenna, 50 Ω | Quick bring-up, known good VSWR | SMA-M |
| Jx | 6 | Edge SMA (vertical/right-angle) | RF in/out, test insert points | Insert Stage A filters & instruments | PCB edge |

### Stage A — Bench / breadboard filters (connectorized)
| Ref | Qty | Part / Option | Description & Key Specs | Use / Why it’s here | Interface |
|---|---:|---|---|---|
| FBA1 | 1 | Mini-Circuits **ZX75BP-915-S+** | Ceramic BPF, ~902.5–927.5 MHz passband | Whole-band preselector on the bench | SMA in-line |
| FBA2 | 1 | Mini-Circuits **ZVBP-909A-S+** | Cavity BPF, ~902–915 MHz | RX chain shaping near 906 MHz | SMA in-line |
| FBA3 | 1 | Southwest Antennas **1080-100/101** | In-line BPF, 902–928 MHz | Simple ISM preselector | SMA or RP-SMA in-line |

### Stage B — On-board ISM preselector (wide SMD)
| Ref | Qty | Part / Option | Description & Key Specs | Use / Why it’s here | Package |
|---|---:|---|---|---|
| FBB1 | 2 | Abracon **AFS915…** / **ABSES5AD-1E3M012M** | SAW BPF, fc≈915 MHz, wide (≈26 MHz) | First-stage OOB suppression | SMD 3×3 mm / 1.4×1.1 mm |
| FBB2 | 2 | Murata **SF2053E** | SAW BPF, usable ≈908.75–921.25 MHz | Wide ISM pass, low IL | SMD |
| FBB3 | 2 | RF360/TDK **B4344 / B3728** | SAW BPF, ISM band, options incl. ~10 MHz PBW | Tighter preselector variant | SMD 3×3 mm |

### Stage C — Channel-select filters (narrower)
| Ref | Qty | Part / Option | Description & Key Specs | Use / Why it’s here | Package |
|---|---:|---|---|---|
| FBC1 | 2 | **906 MHz** BPF options | SAW/Ceramic centered near 906 MHz (examples below) | RX chain (centered near 906) | SMD / Module |
|  |  | Tai-Saw **TA0562A** | SAW, fc≈906 MHz, ~36 MHz BW | Easy to source, medium BW | SMD |
|  |  | Anatech **AM906S530 / AM906B1118** | SAW/Ceramic, 906 MHz; spec variants from ±19 MHz to narrower customs | Path to tighter selectivity | SMD |
| FBC2 | 2 | **920–922.5 MHz** BPF options | SAW centered near 920–922.5 MHz | TX chain (centered near 920) | SMD / Module |
|  |  | ITF **F9201** | SAW, fc≈920 MHz | 920-centered option | SMD |
|  |  | Dynamic Engineers **SF3030AO-920** | BPF centered 920 MHz (~40 MHz BW) | Medium BW option | SMD |

> Tip: If channel-narrow SAWs are hard to buy in singles, keep Stage A (cavity) inline parts to emulate narrow lanes during bring-up, then migrate to Stage C parts later.

---

## RF gain / conversion / LO

| Ref | Qty | Part | Description | Notes | Package |
|---|---:|---|---|---|---|
| LNA1 | 2 | Mini-Circuits **PSA4-5043+** | 50–4000 MHz LNA, NF ≈0.75 dB | Solid 900 MHz choice for RX | SOT-343 |
| MIX1 | 2 | Mini-Circuits **ZFM-2-S+** (bench) | Level-7 DBM, 1–1000 MHz | Connectorized mixer for fast tests | SMA module |
|  | 2 | Mini-Circuits **ADE-12+** (on-board) | Level-7 DBM, 50–1000 MHz | SMD mixer for the PCB | SMD |
| PLL1 | 2 | Analog Devices **ADF4351** | 35 MHz–4.4 GHz frac-N synthesizer | LO for TX & RX | QFN / Dev board |

---

## IF / demod / audio

| Ref | Qty | Part | Description | Notes | Package |
|---|---:|---|---|---|---|
| IF1 | 4 | TDK **FFE1070** / Murata **SFELF/SFTLF 10.7 MHz** | 10.7 MHz ceramic IF filters | Ladder or 2-pole, pick BW for voice | TH or SMD |
| DEM1 | 2 | NXP **SA615 / SA616** | FM IF system (limiter + quadrature det + RSSI) | Classic 10.7 MHz voice IF | SSOP-20 |
| ALT-DEM | 2 | NJM **NJM2591** | FM IF demodulator (450 kHz–10.7 MHz use) | Low-power voice | SOP |
| AUD | 2 | Small class-D amp (e.g., PAM8302) | Audio out to speaker | Any |

---

## Full-duplex isolation helpers

| Ref | Qty | Part | Description | Use | Interface |
|---|---:|---|---|---|---|
| CPL1 | 1 | Mini-Circuits **ZFBDC20-900HP** (or DBTC-7-152X+) | Directional/bidirectional coupler around 900 MHz | TX leak sampling, cancellation experiments, isolation | SMA or SMD |

---

## Passives / matching / power
- 50 Ω microstrip/coplanar lines; 0402/0603 **L/C** kits for matching the SAWs and antenna.
- Low-noise LDOs for RF rails; separate analog and digital grounds where practical.
- Shield cans for RF sections (optional at breadboard stage, recommended for final PCB).

