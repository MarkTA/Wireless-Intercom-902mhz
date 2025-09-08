# Wireless Intercom System (902–928 MHz ISM Band)

## Project Overview
This project is a **custom-designed wireless intercom system** for point-to-point voice communication between two locations (~200 ft apart).  
Unlike off-the-shelf modules, this design explores **RF circuit design, PCB layout, and audio signal processing** from scratch, targeting the 902–928 MHz ISM band.  

The project serves as both a **portfolio piece** and a **hands-on learning exercise** in RF electronics, PCB design, and embedded systems.

---

## Objectives
- Design and build a **two-way wireless intercom** operating in the 902–928 MHz ISM band.  
- Explore **RF front-end design** without relying on modules (no ESP32, no LoRa modules).  
- Practice PCB layout in **Altium Designer** and RF simulation in **Keysight ADS**.  
- Document the design and prototyping process for professional portfolio use.  

---

## Repository Structure

```
/docs
overview.md
design-decisions.md
simulations.md
testing.md
results.md

/hardware
schematics/
pcb-layouts/

/simulations
ads/
ltspice/

/bom
bom.csv
bom.md

/images
block-diagrams/
oscilloscope-screenshots/

/src (optional, for microcontroller code if added later)
```
---

## Tools & Technologies
- **Altium Designer** → schematic capture & PCB layout  
- **Keysight ADS** → RF simulation  
- **LTSpice** → circuit analysis (audio stages, filters)  
- **Oscilloscope & Spectrum Analyzer** → testing and debugging  
- **2-layer PCB fabrication**  

---

## System Block Diagram
*(Insert diagram here once drafted — mic → preamp → modulator → RF front-end → antenna → demodulator → audio out)*

---

## Bill of Materials (BOM)
See [`/bom/bom.md`](./bom/bom.md) for full list.  

Key components include:
- Audio preamp op-amp  
- RF transistors / mixers  
- Band-pass filters  
- Antennas (quarter-wave monopole or custom)  

---

## Current Status
- Frequency band chosen (902–928 MHz ISM)  
- Block diagram in progress  
- Schematic design next  

---

## Future Work
- Prototype on breadboard / perfboard  
- Fabricate PCB and assemble  
- Measure RF performance and audio clarity  
- Explore duplex / push-to-talk modes  

---

## Author
Mark Anderson — Electrical Engineering Student @ ASU  
Passionate about RF, embedded systems, and building from scratch.  

---

## License
MIT License (or your choice)

