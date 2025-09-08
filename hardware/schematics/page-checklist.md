# Schematic Page Checklist — Wireless Intercom (Full-Duplex FDD)

This checklist defines the schematic page breakdown, key nets, reference designators, and bring-up test points (TPs). Use it as the backbone for Altium sheet creation and bring-up planning.

Global nets:
- Power: +12V_IN, +5V, +3V3_RF, +3V3_DIG (optionally +3V3_AUD), GND, GND_RF
- RF: TX_RF, RX_RF, COUP_TAP, CANCEL_VEC, RX_PRESEL_OUT, LNA_OUT, IF, REF_XTAL
- Audio: MIC_RAW, AUDIO_TX, DEMOD_OUT, AUDIO_RX, SPK_DRV, AEC_REF
- Control: PA_EN, MUTE, LOCK_TX, LOCK_RX, I2C/SPI nets to PLLs, SWD/JTAG

---

## Sheet A — Title, Notes, Net Dictionary
- Project title block, revision block, channel plan summary (TX_CF, RX_CF, IF).
- Net legend: list and short description for all global nets.
- Mechanical notes: antenna spacing, ground strategy, shield can locations.

Test Points (TP): none required on this sheet.

---

## Sheet B — Power Entry and Regulation
Blocks:
- DC input jack or battery connector; reverse polarity protection; TVS diode; input EMI filter.
- Buck regulator to +5V.
- LDOs to +3V3_RF and +3V3_DIG (optionally +3V3_AUD). Ferrite beads to isolate rails.
- Decoupling networks and bulk caps per rail.

Key nets: +12V_IN, +5V, +3V3_RF, +3V3_DIG, GND, GND_RF

TPs:
- TP_12VIN (pre-regulator)
- TP_5V
- TP_3V3_RF
- TP_3V3_DIG
- TP_GND_REF (star-point ground reference)

Checklist:
- [ ] Reverse/OV protection sized for supply
- [ ] Input LC/π filter values annotated
- [ ] Bead part numbers and impedance noted
- [ ] Rail ripple/budget comments

---

## Sheet C — TX Audio Front-End and Modulator Interface
Blocks:
- Mic bias and low-noise preamp (gain 20–40 dB).
- HPF ~150–200 Hz, LPF ~3–4 kHz, compressor/AGC.
- Summing node into FM modulator input (varactor or VCO modulation pin).

Key nets: MIC_RAW, AUDIO_TX

TPs:
- TP_MIC (mic preamp output)
- TP_AUD_TX_IN (audio into modulator)
- TP_DEV_MON (optional detector to observe FM deviation)

Checklist:
- [ ] Noise/gain budgeting annotated
- [ ] Input impedance and bias network values
- [ ] Provision for gain trim or jumper

---

## Sheet D — TX LO/PLL, Buffer, SAW, PA, Antenna
Blocks:
- TX VCO/PLL with REF_XTAL, loop filter, SPI/I2C control.
- TX buffer/driver, matching network.
- TX SAW band-pass filter centered at TX_CF.
- PA stage set initially for +0 to +5 dBm.
- ANT-TX connector (edge-launch SMA or PCB antenna footprint).

Key nets: TX_RF, REF_XTAL, LOCK_TX, PA_EN

TPs:
- TP_TX_LO (VCO/PLL RF out before buffer)
- TP_TX_POST_BPF (after TX SAW)
- TP_TX_OUT (at PA output / feedline to ANT-TX)

Checklist:
- [ ] Loop filter values calculated and documented
- [ ] Matching networks simulated (S-params if available)
- [ ] Harmonic filter or low-pass after PA if needed

---

## Sheet E — Antennas and Optional Analog Cancellation (v2+)
Blocks:
- ANT-TX and ANT-RX footprints with spacing/cross-pol notes.
- Optional: directional coupler on TX line, variable attenuator, tunable phase shifter, 180° hybrid/combiner injecting into RX path pre-LNA.

Key nets: TX_RF, RX_RF, COUP_TAP, CANCEL_VEC

TPs:
- TP_COUP_TAP (sampled TX for cancellation)
- TP_CANCEL_VEC (post attenuator/phase)
- TP_RX_IN_RAW (RX feed just before RX SAW/limiter)

Checklist:
- [ ] Mechanical callouts for antenna placement
- [ ] If cancellation omitted for v1, include DNP notes and jumpers

---

## Sheet F — RX Front-End: Preselector, Limiter, LNA, Mixer
Blocks:
- RX SAW preselector centered at RX_CF.
- RF limiter/attenuator to protect LNA.
- LNA with appropriate bias/matching.
- Mixer to chosen IF (e.g., 10.7 MHz).
- RX VCO/PLL with REF_XTAL, control lines.

Key nets: RX_RF, RX_PRESEL_OUT, LNA_OUT, IF, REF_XTAL, LOCK_RX

TPs:
- TP_RX_POST_SAW (after RX SAW)
- TP_LNA_OUT
- TP_IF_IN (mixer output to IF filter)
- TP_RX_LO (optional LO monitor via high-Z pad)

Checklist:
- [ ] SAW insertion loss and skirt specs annotated
- [ ] LNA bias currents and stability network
- [ ] Mixer LO drive level noted

---

## Sheet G — IF Filter and FM Demodulator
Blocks:
- IF band-pass filter (e.g., 10.7 MHz ceramic ladder) with matching.
- FM demodulator (quadrature discriminator or PLL-based) and de-emphasis.
- Level shifting to audio chain.

Key nets: IF, DEMOD_OUT, AUDIO_RX

TPs:
- TP_IF (post-filter IF node)
- TP_DEMOD_OUT (baseband audio before DSP)

Checklist:
- [ ] IF bandwidth chosen for speech + deviation
- [ ] Discriminator alignment notes (if coil-based)
- [ ] De-emphasis time constant documented

---

## Sheet H — Audio Output, AEC/DSP, Speaker Amp
Blocks:
- ADC/DAC or audio codec if MCU converters are insufficient; MCU/DSP for AEC (NLMS), AGC.
- Speaker amplifier and output protection; optional headphone jack with detect.
- AEC reference pick-off from SPK_DRV.

Key nets: DEMOD_OUT, AUDIO_RX, AEC_REF, SPK_DRV, +3V3_DIG (or +5V for amp)

TPs:
- TP_AUD_RX (audio into DSP)
- TP_AEC_REF (speaker drive reference to DSP)
- TP_SPK_DRIVE (amp input)
- TP_SPK_OUT (to speaker terminals)

Checklist:
- [ ] Codec clocking domain and grounding
- [ ] AEC processing rate and memory notes
- [ ] Gain staging to avoid clipping

---

## Sheet J — Digital Control, Programming, Indicators
Blocks:
- MCU, SWD/JTAG header, boot jumpers.
- I2C/SPI buses to TX/RX PLLs; GPIOs for PA_EN, MUTE, LEDs.
- Configuration EEPROM (optional).

Key nets: PA_EN, MUTE, SPI_*/I2C_*, LOCK_TX, LOCK_RX, SWD/JTAG

TPs:
- TP_SWDIO, TP_SWCLK (or equivalent)
- TP_I2C_SCL/SDA or SPI_SCLK/MOSI/MISO
- TP_LOCK_TX, TP_LOCK_RX (optional LED test pads)

Checklist:
- [ ] Pull-ups/pull-downs per bus requirements
- [ ] Programming header orientation and keep-out
- [ ] Status LED current-limit values

---

## Bring-Up Sequence (recommended)
1) Sheet B: Validate rails and ripple at TP_12VIN / TP_5V / TP_3V3_*.
2) Sheet D: Bring up TX LO/PLL into a 50 Ω load; verify frequency, phase noise, deviation at TP_TX_LO / TP_TX_POST_BPF / TP_TX_OUT.
3) Sheet F/G: Inject RF at ANT-RX or TP_RX_POST_SAW; verify IF and demod at TP_IF and TP_DEMOD_OUT.
4) Sheet C/H: Validate audio paths with PTT operation first; then enable AEC and confirm stability at TP_AUD_RX / TP_AEC_REF.
5) Sheet E (if installed): Tune cancellation vector; measure null at TP_RX_IN_RAW; document dB isolation.

