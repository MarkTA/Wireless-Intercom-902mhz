# Full-Duplex Plan (902–928 MHz)

## Goals
- Achieve simultaneous talk/listen over ~200 ft using two channels within 902–928 MHz.
- Maintain intelligible audio with minimal self-interference and low audible echo.

## Channel Plan
- Example: Node A TX @ 906 MHz, RX @ 920 MHz; Node B TX @ 920 MHz, RX @ 906 MHz.
- Frequency separation target: ≥5–10 MHz to ease filtering.

## Isolation Budget (illustrative)
- TX power initial target: +0 to +5 dBm.
- Required cumulative TX→RX isolation (goal): ≥100 dB for comfortable margin.
  - SAW bandpass (each path): 50–70 dB rejection at the opposite channel
  - Antenna isolation: 20–30 dB via spacing (≥30–50 cm), cross-pol, and placement
  - Optional analog RF cancellation: 20–40 dB when tuned
  - Front-end limiter to protect LNA if residual is high

## RF Building Blocks
- **Filters:** Pair of SAW/ceramic BPFs centered on each channel; sharp skirts to suppress the other channel.
- **Coupler & Cancellation (optional):** Directional coupler (−10 to −20 dB tap), variable attenuator, tunable phase shifter (LC all-pass or vector modulator), 180° combiner into RX input.
- **Antennas:** Two per node, separated physically and/or cross-polarized. Start with quarter-wave monopoles; consider a small ground plane.

## Receiver Protection and Linearity
- Input limiter (e.g., RF limiter diode network) before LNA.
- Choose LNA with adequate IP3 and P1dB; keep early gains moderate.

## Audio Signal Path and Echo Control
- **AEC:** NLMS at 8–16 kHz sampling; mic input as primary, speaker drive as reference.
- **Signal conditioning:** High-pass ~150–200 Hz, low-pass ~3–4 kHz, mild compression, AGC, optional noise gate.
- **Mechanical:** Mic baffle, absorbent lining, mic/speaker offset and orientation.

## Bring-Up Strategy
1. **Bench RF only:** Verify filter responses and antenna isolation with a VNA. Record S-parameters.  
2. **Low-power TX:** Start at minimum TX power; verify RX sensitivity isn’t crushed.  
3. **Add cancellation (if used):** Tune attenuator/phase for a null at the RX port; document achieved dB.  
4. **Audio path (PTT first):** Validate audio chains; then enable AEC and confirm stability.  
5. **Integration tests:** Measure SINAD/voice intelligibility, end-to-end latency, and stability under movement.

## Test Metrics to Log
- TX→RX leakage at RX input (dBm) vs frequency.
- Achieved isolation (dB) by mechanism (filter, antenna, cancellation).
- RX sensitivity with and without self-interference active.
- AEC convergence time and residual echo (ERLE in dB).
- End-to-end latency and subjective voice quality.

## Open Questions / To Decide
- Exact SAW part numbers and center frequencies.
- Whether to include analog RF cancellation on the first spin or keep it for v2.
- Final enclosure layout for best acoustic and RF isolation.
