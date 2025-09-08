# Block Diagrams — Wireless Intercom (Full-Duplex FDD, 902–928 MHz)

This document captures high-level and detailed block diagrams for a single node in the full-duplex intercom. Each node simultaneously transmits on one ISM sub-channel and receives on another (e.g., TX at 906 MHz, RX at 920 MHz). Physical antenna separation, sharp filtering, and careful gain planning are used to control self-interference.

---

## 1) High-Level Node Diagram

Mic → Preamp/Filters → FM Modulator → TX LO/VCO/PLL → TX Buffer/PA → TX SAW BPF → ANT-TX
                                                                                │
                                                                                │  (spatial separation / cross-pol)
                                                                                ▼
ANT-RX → RX SAW Preselector → RF Limiter → LNA → Mixer/Downconversion ← RX LO/VCO/PLL
                                         │
                                         └─→ IF BPF → FM Demod → De-emphasis/Filters → AEC/AGC → Speaker Amp → Speaker

Control/DSP: MCU for AEC, gain/mute control, PLL programming, status LEDs
Power: DC input → 5 V buck → 3.3 V LDOs (separate rails for RF and digital/audio)

Notes:
- Full-duplex via frequency-division duplexing (FDD) inside the 902–928 MHz ISM band.
- Optional analog RF cancellation can be inserted between ANT-RX and LNA (not required for v1).

---

## 2) RF Focused Diagram (with optional cancellation)

                 ┌──────────────────────────────────────── TX PATH ─────────────────────────────────────────┐
Mic → Pre/HPF/LPF/AGC → FM Mod In → TX VCO/PLL → TX Buffer → TX SAW BPF → PA → ANT-TX → free space
                 └──────────────────────────────────────────────────────────────────────────────────────────┘

                 ┌──────────────────────────────────────── RX PATH ─────────────────────────────────────────┐
free space → ANT-RX → RX SAW Preselector → (optional cancel injection node) → Limiter → LNA → Mixer → IF
                                                                                             │
                                                                                 RX LO/VCO/PLL
                                                                                             │
                                                                                   IF BPF → Demod → Audio chain
                 └──────────────────────────────────────────────────────────────────────────────────────────┘

Optional analog cancellation (v2+):
- Directional coupler samples TX line → variable attenuator → tunable phase shifter → 180° combiner → inject at RX input before LNA.

---

## 3) Audio/DSP Chain

Mic → Low-noise preamp (gain 20–40 dB) → HPF ~150–200 Hz → LPF ~3–4 kHz → Compressor/AGC
  → FM modulator input

Demodulated audio → De-emphasis/LPF → AEC (NLMS) with reference = speaker drive → AGC → Speaker amp → Speaker

---

## 4) Control, Clocking, and Power

- Reference crystal for PLLs and MCU.
- I2C/SPI control for TX/RX PLLs, GPIO for PA enable and muting.
- Power domains: +12 V input → 5 V buck → split LDOs to 3V3_RF and 3V3_DIG (optionally 3V3_AUD).
- Grounding: star-point RF ground, keep RF return currents local; separate analog/digital grounds with a single-point tie.

---

## 5) Suggested Channel Plan (initial)

- Node A: TX @ 906 MHz, RX @ 920 MHz
- Node B: TX @ 920 MHz, RX @ 906 MHz
- Deviation: ±2.5 kHz (start), audio BW ~3 kHz, can widen later to ±5 kHz if filtering allows.

