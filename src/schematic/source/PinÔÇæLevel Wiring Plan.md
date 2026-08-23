# Ohio Scientific Superboard II – Pin‑Level Wiring Plan
### KiCad 10 Builder‑Friendly Edition

This document defines **pin‑accurate net labels** for every major IC on each schematic sheet.  
Use this alongside the sheet‑by‑sheet net‑label plan to wire the entire board unambiguously.

---

# Sheet 1 — CPU, ROM, ACIA, Core Decode

## U8 — 6502 CPU (DIP‑40)

### Address Bus
- Pin 9  → `A0`
- Pin 10 → `A1`
- Pin 11 → `A2`
- Pin 12 → `A3`
- Pin 13 → `A4`
- Pin 14 → `A5`
- Pin 15 → `A6`
- Pin 16 → `A7`
- Pin 17 → `A8`
- Pin 18 → `A9`
- Pin 19 → `A10`
- Pin 20 → `A11`
- Pin 21 → `A12`
- Pin 22 → `A13`
- Pin 23 → `A14`
- Pin 24 → `A15`

### Data Bus
- Pin 33 → `D0`
- Pin 32 → `D1`
- Pin 31 → `D2`
- Pin 30 → `D3`
- Pin 29 → `D4`
- Pin 28 → `D5`
- Pin 27 → `D6`
- Pin 26 → `D7`

### Control
- Pin 34 → `R_W`
- Pin 37 → `PHI2`
- Pin 4  → `IRQ`
- Pin 6  → `NMI`
- Pin 40 → `RESET`

### Power
- Pin 1  → `GND`
- Pin 8  → `GND`
- Pin 35 → `+5V`

---

## U9–U12 — BASIC ROMs (2716/2732 EPROM)

### Address Inputs
- A0 → Pin 9  
- A1 → Pin 10  
- A2 → Pin 11  
- A3 → Pin 12  
- A4 → Pin 13  
- A5 → Pin 14  
- A6 → Pin 15  
- A7 → Pin 16  
- A8 → Pin 17  
- A9 → Pin 18  
- A10 → Pin 19  

### Data Outputs
- D0 → Pin 8  
- D1 → Pin 7  
- D2 → Pin 6  
- D3 → Pin 5  
- D4 → Pin 4  
- D5 → Pin 3  
- D6 → Pin 2  
- D7 → Pin 1  

### Control
- `CS_BASICx` → Pin 20  
- `OE_ROM`    → Pin 21  

### Power
- Pin 24 → `+5V`
- Pin 12 → `GND`

---

## U13 — Monitor ROM (same pinout as above)
Use:
- `CS_MONITOR` → Pin 20  
- Same address/data/control mapping as BASIC ROMs.

---

## U14 — 6850 ACIA (DIP‑24)

### Data Bus
- D0 → Pin 19  
- D1 → Pin 18  
- D2 → Pin 17  
- D3 → Pin 16  
- D4 → Pin 15  
- D5 → Pin 14  
- D6 → Pin 13  
- D7 → Pin 12  

### Control
- `CS_ACIA` → Pin 11  
- `R_W`     → Pin 10  
- `ACIA_CLK` → Pin 9  

### Serial I/O
- `TX_DATA` → Pin 7  
- `RX_DATA` → Pin 6  
- `CTS`     → Pin 5  
- `RTS`     → Pin 4  

### Power
- Pin 24 → `+5V`
- Pin 1  → `GND`

---

## U17 — 74LS139 (Dual 2‑to‑4 Decoder)

### Decoder A
- A0 → Pin 2  
- A1 → Pin 3  
- Enable → Pin 1  
- Outputs → Pins 4, 5, 6, 7 (`SEL_*` nets)

### Decoder B
- A0 → Pin 14  
- A1 → Pin 13  
- Enable → Pin 15  
- Outputs → Pins 12, 11, 10, 9

---

## U20, U22, U23 — 74LS138 (3‑to‑8 Decoder)

### Inputs
- A0 → Pin 1  
- A1 → Pin 2  
- A2 → Pin 3  

### Enables
- G1  → Pin 6  
- G2A → Pin 4  
- G2B → Pin 5  

### Outputs
- Y0–Y7 → Pins 7–9, 10–12, 13–15  
Map these to:
- `CS_BASICx`  
- `CS_MONITOR`  
- `CS_RAMx`  
- `CS_IO`  
- `CS_VIDEO`

---

# Sheet 2 — RAM, Bus Buffers, Additional Decode

## U31–U40, U45–U52 — 2114 SRAM (DIP‑18)

### Address Inputs
- A0 → Pin 9  
- A1 → Pin 10  
- A2 → Pin 11  
- A3 → Pin 12  
- A4 → Pin 13  
- A5 → Pin 14  
- A6 → Pin 15  

### Data I/O
- D0 → Pin 8  
- D1 → Pin 7  
- D2 → Pin 6  
- D3 → Pin 5  

### Control
- `CS_RAMx` → Pin 16  
- `RAM_WE_N` → Pin 3  
- `RAM_OE_N` → Pin 2  

### Power
- Pin 1 → `+5V`  
- Pin 18 → `GND`

---

## U24–U25 — 8T28 Bus Transceivers (use 74xx octal buffer symbol)

### Data Bus Side
- D0–D7 → Pins 2–9

### Buffered Side
- BD0–BD7 → Pins 11–18

### Control
- `BUF_EN_DATA` → Pin 1  
- `BUF_DIR`     → Pin 19  

### Power
- Pin 20 → `+5V`  
- Pin 10 → `GND`

---

# Sheet 3 — Keyboard Logic & Interface

## U42 — 74LS165 (Parallel‑In Serial‑Out)

### Parallel Inputs
- KEY_COL0 → Pin 11  
- KEY_COL1 → Pin 12  
- KEY_COL2 → Pin 13  
- KEY_COL3 → Pin 14  
- KEY_COL4 → Pin 3  
- KEY_COL5 → Pin 4  
- KEY_COL6 → Pin 5  
- KEY_COL7 → Pin 6  

### Serial
- `KEY_DATA_OUT` → Pin 9  

### Control
- `KEY_CLK`     → Pin 2  
- `KEY_LOAD_N`  → Pin 1  

### Power
- Pin 16 → `+5V`  
- Pin 8  → `GND`

---

## U65, U69 — 74123 (Monostable)

### Inputs
- Trigger A → Pin 1  
- Trigger B → Pin 2  
- Clear     → Pin 3  

### Output
- `KEY_DEBOUNCE` or `BREAK_PULSE` → Pin 6  

### Power
- Pin 14 → `+5V`  
- Pin 7  → `GND`

---

# Sheet 4 — Video Generation & Timing

## U41 — Character Generator ROM

### Address Inputs
- ROW_ADDR0–ROW_ADDRn → Pins 9–?  
- COL_ADDR0–COL_ADDRm → Pins 10–?  

### Data Outputs
- CHAR_CODE0–7 → Pins 1–8  

### Control
- `CS_CARGEN` → Pin 20  
- `OE_CARGEN` → Pin 21  

### Power
- Pin 24 → `+5V`  
- Pin 12 → `GND`

---

## U53–U55 — 74LS157 (Quad 2‑to‑1 Mux)

### Inputs
- A0–A3 → Pins 2, 5, 11, 14  
- B0–B3 → Pins 3, 6, 10, 13  

### Select
- `VID_SEL` → Pin 1  

### Outputs
- VID_DATA0–3 → Pins 4, 7, 9, 12  

### Power
- Pin 16 → `+5V`  
- Pin 8  → `GND`

---

## U30, U57, U59–U61 — 74LS163 (Counters)

### Inputs
- CLK → Pin 2 (`DOT_CLK`)  
- CLEAR → Pin 1 (`RESET_N`)  
- LOAD → Pin 9  
- ENABLE → Pins 7, 10  

### Outputs
- H_COUNTx / V_COUNTx → Pins 11, 12, 13, 14  

### Power
- Pin 16 → `+5V`  
- Pin 8  → `GND`

---

## U66 — CA3130 Op‑Amp

### Inputs
- VID_RAW → Pin 3  
- VID_REF → Pin 2  

### Output
- VIDEO_OUT → Pin 6  

### Power
- Pin 7 → `+5V`  
- Pin 4 → `GND`

---

# Sheet 5 — Power, DAC, Misc I/O

## D15 — 1N4001 Rectifier
- Anode → `PWR_IN_RAW`  
- Cathode → `PWR_IN`

## F1 — Fuse
- Input → `PWR_IN`  
- Output → `+5V`

## DAC / Noise
- `DAC_OUT`  
- `DAC_DISABLE`  
- `NOISE`  
- `WKB`

---

# Global Wiring Rules

### Use global labels for:
- `A0–A15`
- `D0–D7`
- `PHI2`
- `R_W`
- `RESET`
- `IRQ`, `NMI`
- `TX_DATA`, `RX_DATA`, `CTS`, `RTS`
- `HSYNC`, `VSYNC`, `COMP_SYNC`, `VIDEO_OUT`
- `KEY_ROWx`, `KEY_COLx`
- `DAC_OUT`, `DAC_DISABLE`, `NOISE`
- `+5V`, `GND`

### Use local labels for:
- `SEL_*`
- `CS_RAMx`
- `VID_RAW`, `VID_REF`
- `KEY_DEBOUNCE`, `BREAK_PULSE`
- `BUF_EN_DATA`, `LATCH_OUTx`

---

# Next Step
If you want, I can generate **KiCad‑ready symbol placement templates** for each sheet so you can drop symbols in the correct order and wire them immediately.
