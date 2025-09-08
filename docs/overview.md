# Project Overview: Wireless Intercom System (902–928 MHz ISM Band)

## Introduction
This project explores the design and implementation of a point-to-point wireless intercom system. The intended use case is communication between a shop and a house located approximately 200 feet apart. Unlike commercial intercoms that rely on off-the-shelf RF modules, this project is focused on building the RF and audio stages from the ground up.  

The design will use the 902–928 MHz ISM band, which is license-free in the United States and suitable for short-range wireless communication.

---

## Motivation
- Gain hands-on experience with RF circuit design and testing.  
- Build familiarity with PCB design in Altium Designer.  
- Apply simulation tools such as Keysight ADS and LTSpice.  
- Develop a project suitable for inclusion in a professional engineering portfolio.  

---

## System Requirements
- Range: approximately 200 feet (line of sight).  
- Power: low-power operation, battery or DC supply.  
- Audio quality: intelligible voice communication (not necessarily hi-fi).  
- Duplex mode: either half-duplex (push-to-talk) or full-duplex depending on complexity.  
- Robustness: must work reliably in an environment with moderate RF noise.  

---

## High-Level Design Concept
1. **Microphone Input Stage**  
   - Electret microphone or condenser mic element.  
   - Preamp for boosting low-level audio signal.  

2. **Modulation Stage**  
   - Analog modulation scheme (likely FM for voice quality).  
   - Option to explore AM for simplicity in early prototypes.  

3. **RF Front-End (TX)**  
   - Local oscillator operating in the 902–928 MHz range.  
   - Mixer for upconversion of modulated signal.  
   - Band-pass filter for spectral compliance.  
   - Power amplifier (low power, < 1 W).  

4. **Antenna**  
   - Quarter-wave monopole or dipole tuned to ~915 MHz.  

5. **RF Front-End (RX)**  
   - Band-pass filter and low-noise amplifier.  
   - Mixer with local oscillator for downconversion.  
   - IF filter and amplifier stage.  
   - Detector/demodulator.  

6. **Audio Output Stage**  
   - Amplifier suitable for driving a small speaker.  

---

## Design Tools
- **Altium Designer** for schematic capture and PCB layout.  
- **Keysight ADS** for RF block simulations.  
- **LTSpice** for audio preamp and filter analysis.  
- **Oscilloscope / Spectrum Analyzer** for real-world measurements.  

---

## Constraints and Challenges
- Ensuring compliance with FCC Part 15 rules for ISM band devices.  
- Designing stable oscillators and mixers without relying on integrated modules.  
- Balancing complexity with available tools and budget.  
- Avoiding interference with other ISM band devices (Wi-Fi, cordless phones, etc.).  

---

## Current Status
- Frequency band selected (902–928 MHz ISM).  
- Block diagram drafted.  
- Next step: audio preamp design and modulation scheme evaluation.  

---

## Next Steps
1. Finalize block diagram with chosen modulation scheme.  
2. Begin audio preamp design in LTSpice.  
3. Research oscillator topologies (Colpitts, Clapp, etc.) for the RF front-end.  
4. Document preliminary Bill of Materials (BOM).  

---

## Long-Term Goals
- Assemble a working prototype on perfboard.  
- Fabricate and test a 2-layer PCB version.  
- Create a polished portfolio report with schematics, test results, and design decisions.  
- Demonstrate reliable voice communication over 200 feet.  
