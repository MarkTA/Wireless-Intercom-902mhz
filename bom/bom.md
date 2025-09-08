# Bill of Materials — Budget Mode (902–928 MHz, Full-Duplex: TX≈920 / RX≈906)

**Goal:** keep per-node RF parts inexpensive while preserving a clean path to full-duplex.  
**Strategy:** stack isolation from (1) big channel split, (2) **cascaded low-cost SAW filters**, (3) antenna spacing/cross-pol, and (4) low TX power during bring-up.

- **Default (v1)**: two **wide ISM SAWs in cascade** per path (TX and RX).
- **Optional (v1.1+)**: add a **channel-centered SAW** in the RX@906 path and/or TX@920 path for more isolation (mark as **DNP** until needed).
- **No pricey cavity filters** required.

---

## RF Filtering Plan (per node)

- **TX path (≈920 MHz)**  
  1) Wide ISM SAW (915 MHz class) →  
  2) Wide ISM SAW (second stage, cascade) →  
  3) PA → ANT-TX  
  *Optional:* After bring-up, replace the second wide SAW with a 920-centered SAW.

- **RX path (≈906 MHz)**  
  1) Wide ISM SAW (915 MHz class) →  
  2) Wide ISM SAW (second stage, cascade) →  
  3) Limiter → LNA → Mixer  
  *Optional:* Replace the second wide SAW with a 906-centered SAW for tighter selectivity.

**Why cascades?** Two low-cost SAWs typically give noticeably better out-of-band rejection than one, for just a few dollars total.

---

## Bill of Materials (per node)

### Antennas & RF I/O
| Ref | Qty | Part / Class | Description | Notes |
|---|---:|---|---|---|
| ANT1 | 1 | ¼-wave @ ~915 MHz | Wire or whip antenna, 50 Ω | TX antenna (cheap start: straight wire cut ≈8.2 cm) |
| ANT2 | 1 | ¼-wave @ ~915 MHz | Wire or whip antenna, 50 Ω | RX antenna (try cross-pol vs TX for isolation) |
| J1..J6 | 6 | Edge-launch SMA | PCB edge SMA connectors | For test points and modular bring-up (optional, can reduce qty) |

### SAW Band-Pass Filters (low-cost)
| Ref | Qty | Part (example family) | Center | PBW (approx) | Package | Use |
|---|---:|---|---|---|---|---|
| FBB_TX1 | 1 | 915 MHz ISM SAW (e.g., RF360/TDK B3728 class) | ~915 | wide ISM | SMD | TX pre-select stage 1 |
| FBB_TX2 | 1 | 915 MHz ISM SAW (same family) | ~915 | wide ISM | SMD | TX pre-select stage 2 (cascade) |
| FBB_RX1 | 1 | 915 MHz ISM SAW (e.g., RF360/TDK B3728 class) | ~915 | wide ISM | SMD | RX pre-select stage 1 |
| FBB_RX2 | 1 | 915 MHz ISM SAW (same family) | ~915 | wide ISM | SMD | RX pre-select stage 2 (cascade) |
| FBC_RX | 1 | ~906 MHz SAW (optional) | ~906 | medium | SMD | **DNP v1**; swap in for RX stage 2 if needed |
| FBC_TX | 1 | ~920 MHz SAW (optional) | ~920 | medium | SMD | **DNP v1**; swap in for TX stage 2 if needed |

> You can build v1 with only the four wide SAWs (FBB_*). Add the channel-centered parts later if you need more isolation.

### RX Front-End / Conversion
| Ref | Qty | Part | Notes |
|---|---:|---|---|
| LNA1 | 1 | 900 MHz LNA (e.g., Mini-Circuits PSA4-5043+ class) | Low NF front-end gain stage |
| MIX1 | 1 | Level-7 diode ring mixer (e.g., ADE-12+ class) | 50–1000 MHz coverage |
| LMT1 | 1 | RF limiter / protector | Protects LNA from TX leakage (small SOT limiter or PIN pair) |

### Local Oscillators / Synthesizers
| Ref | Qty | Part | Notes |
|---|---:|---|---|
| PLL_RX | 1 | Synth/PLL (e.g., ADF4351 board or IC) | RX LO for down-conversion to IF=10.7 MHz |
| PLL_TX | 1 | Synth/PLL (e.g., ADF4351 board or IC) | TX LO / FM VCO path (varactor FM input) |
| XTAL | 1 | Reference crystal (per PLL/MCU req.) | Stability budget for deviation/lock |

### IF & Demodulation (10.7 MHz)
| Ref | Qty | Part | Notes |
|---|---:|---|---|
| IF1..IF2 | 2 | 10.7 MHz ceramic BPFs | Pick bandwidth for voice FM (e.g., 150–280 kHz) |
| DEM1 | 1 | FM IF/demod IC (e.g., NXP SA615/SA616 class) | Limiter + quadrature detector; classic voice IF |

### Audio Chain
| Ref | Qty | Part | Notes |
|---|---:|---|---|
| MIC1 | 1 | Electret or MEMS mic | Cardioid preferred for acoustic isolation |
| PRE1 | 1 | Low-noise op-amp | Mic preamp; gain ≈20–40 dB |
| FILA1 | 1 | HPF/LPF network | ~150–200 Hz HPF, ~3–4 kHz LPF |
| DSP1 | 1 | MCU w/ DSP (Cortex-M4F/M7 class) | AEC (NLMS), AGC, control |
| AMP1 | 1 | Small class-D (e.g., PAM8302 class) | 0.5–3 W speaker driver |
| SPK1 | 1 | Small 4–8 Ω speaker | Enclosure-friendly |

### Power & Control
| Ref | Qty | Part | Notes |
|---|---:|---|---|
| PWR1 | 1 | DC jack or battery connector | 9–12 V input |
| DC1 | 1 | Buck regulator to 5 V | ≥1–2 A, low ripple |
| LDO_RF | 1 | 3.3 V low-noise LDO | RF/PLL rail |
| LDO_DIG | 1 | 3.3 V LDO | MCU / logic |
| UI1 | 1
