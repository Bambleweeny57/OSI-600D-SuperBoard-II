# Ohio Scientific Superboard II – KiCad 10 Schematic Symbol Plan
### Builder‑Friendly Hierarchical Sheet Layout (Standard KiCad Libraries)

This document defines the symbol placement for rebuilding the Superboard II schematic in KiCad 10 using only standard libraries:
- `74xx`
- `Device`
- `Analog`
- `Memory`
- `MCU`
- `Interface_UART`

---

## Sheet 1 — CPU, ROM, ACIA, Core Decode

### IC Symbols
- **U8** — 6502 CPU  
  - Library: `MCU`  
  - Symbol: `6502`
- **U9–U12** — BASIC ROMs 1–4  
  - Library: `Memory_EPROM`  
  - Symbol: `2716` / `2732` (24‑pin EPROM)
- **U13** — Monitor ROM (SYN600)  
  - Library: `Memory_EPROM`
- **U14** — 6850 ACIA  
  - Library: `Interface_UART`
- **U15** — 74LS02 (quad NOR)  
  - Library: `74xx`
- **U16, U18, U21** — 74LS04 (hex inverter)  
  - Library: `74xx`
- **U17** — 74LS139 (dual 2‑to‑4 decoder)  
  - Library: `74xx`
- **U19** — 74LS20 (dual 4‑input NAND)  
  - Library: `74xx`
- **U20, U22, U23** — 74LS138 (3‑to‑8 decoder)  
  - Library: `74xx`

### Passives & Discretes
- Decoupling capacitors: `C21–C59` (0.1 µF)  
  - Library: `Device:C_Small`
- Reset/clock resistors & timing caps  
  - Library: `Device:R`, `Device:C_Small`
- Diodes: 1N914, 1N4001  
  - Library: `Device:D_Small`, `Device:D_Rectifier`

---

## Sheet 2 — RAM, Bus Buffers, Additional Decode

### IC Symbols
- **U31–U40, U45–U52** — 2114 SRAM  
  - Library: `Memory_RAM`
- **U24–U25** — 8T28 bus transceivers  
  - Library: `74xx` (octal buffer)
- **U2–U3** — 74LS75 latches  
  - Library: `74xx`
- **U4–U5** — 74LS125 bus buffers  
  - Library: `74xx`

### Passives
- Decoupling capacitors near each IC  
- Pull‑ups/pull‑downs from resistor schedule  
  - Library: `Device:R`

---

## Sheet 3 — Keyboard Logic & Interface

### IC Symbols
- **U42** — 74LS165 (parallel‑in serial‑out shift register)  
  - Library: `74xx`
- **U43** — 7408 (quad AND)  
  - Library: `74xx`
- **U63** — 7474 (dual D‑flip‑flop)  
  - Library: `74xx`
- **U64** — 74LS76 (JK flip‑flop)  
  - Library: `74xx`
- **U65, U69** — 74123 (monostable multivibrator)  
  - Library: `74xx`
- **U70** — 7403 (open‑collector NAND)  
  - Library: `74xx`

### Discretes
- **D1–D10, D16–D20** — 1N914  
  - Library: `Device:D_Small`
- **Q1, Q2** — 2N5225 / 2N5226  
  - Library: `Device:Q_NPN`, `Device:Q_PNP`
- Keyboard matrix resistors  
  - Library: `Device:R`

---

## Sheet 4 — Video Generation & Timing

### IC Symbols
- **U41** — Character generator ROM  
  - Library: `Memory_ROM` or `Memory_EPROM`
- **U53–U55** — 74LS157 (quad 2‑to‑1 mux)  
  - Library: `74xx`
- **U30, U57, U59–U61** — 74LS163 (counters)  
  - Library: `74xx`
- **U56** — 74LS20 (NAND)  
  - Library: `74xx`
- **U62** — 7404 (hex inverter)  
  - Library: `74xx`
- **U66** — CA3130 op‑amp  
  - Library: `Analog_OpAmp`

### Passives
- Video path resistors (R52–R66 etc.)  
  - Library: `Device:R`
- Timing capacitors (C6–C13, C57)  
  - Library: `Device:C_Small`
- Trimmers (R57, R58)  
  - Library: `Device:R_Potentiometer`

---

## Sheet 5 — Power, DAC, Misc I/O

### Symbols
- **F1** — 5 A fuse  
  - Library: `Device:Fuse`
- **D15** — 1N4001 rectifier  
  - Library: `Device:D_Rectifier`
- **Q1/Q2** (if reused in DAC/noise section)  
  - Library: `Device:Q_NPN`, `Device:Q_PNP`
- Remaining logic ICs used in DAC/noise  
  - Library: `74xx`

### Passives
- Bulk electrolytics (C‑506 series)  
  - Library: `Device:CP_Electrolytic`
- Remaining resistors (R56–R62A, R72 etc.)  
  - Library: `Device:R`
- Remaining bypass caps (CB‑10410)  
  - Library: `Device:C_Small`

---

## Notes for KiCad 10 Rebuild

1. Create the 5 hierarchical sheets listed above.  
2. Place symbols exactly as listed.  
3. Use original net names (`A0–A15`, `D0–D7`, `Φ2`, `R/W`, `RESET`, `VID`, `COMP_SYNC`).  
4. Run ERC per sheet.  
5. Update PCB from schematic.  
6. Align footprints over imported Gerbers and lock them.

---

## Optional Next Step
If you want, I can generate a **Sheet 1 net‑label plan** (CPU + ROM + ACIA + decode) so you can wire the first sheet with zero ambiguity.

Just say the word.
