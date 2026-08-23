# Ohio Scientific Superboard II – KiCad 10 Connection List
### Fully Explicit Net–to–Pin Map for 5 Hierarchical Sheets

Use this as the master “wiring truth” for generating the `.kicad_sch` files.  
Labels follow the net‑label and pin‑level plans you already have.   

---

## Sheet 1 — `CPU_ROM_ACIA` (CPU, ROM, ACIA, Core Decode)

### U8 — 6502 CPU (DIP‑40)

**Address bus**

- **Pin 9:** `A0`  
- **Pin 10:** `A1`  
- **Pin 11:** `A2`  
- **Pin 12:** `A3`  
- **Pin 13:** `A4`  
- **Pin 14:** `A5`  
- **Pin 15:** `A6`  
- **Pin 16:** `A7`  
- **Pin 17:** `A8`  
- **Pin 18:** `A9`  
- **Pin 19:** `A10`  
- **Pin 20:** `A11`  
- **Pin 21:** `A12`  
- **Pin 22:** `A13`  
- **Pin 23:** `A14`  
- **Pin 24:** `A15`  

**Data bus**

- **Pin 33:** `D0`  
- **Pin 32:** `D1`  
- **Pin 31:** `D2`  
- **Pin 30:** `D3`  
- **Pin 29:** `D4`  
- **Pin 28:** `D5`  
- **Pin 27:** `D6`  
- **Pin 26:** `D7`  

**Control / interrupts / clock**

- **Pin 34:** `R_W`  
- **Pin 37:** `PHI2`  
- **Pin 4:** `IRQ`  
- **Pin 6:** `NMI`  
- **Pin 40:** `RESET`  

**Power / ground**

- **Pin 1:** `GND`  
- **Pin 8:** `GND`  
- **Pin 35:** `+5V`  

---

### U9–U12 — BASIC ROMs (2716/2732 EPROM)

**Address inputs**

- **Pin 9:** `A0`  
- **Pin 10:** `A1`  
- **Pin 11:** `A2`  
- **Pin 12:** `A3`  
- **Pin 13:** `A4`  
- **Pin 14:** `A5`  
- **Pin 15:** `A6`  
- **Pin 16:** `A7`  
- **Pin 17:** `A8`  
- **Pin 18:** `A9`  
- **Pin 19:** `A10`  

**Data outputs**

- **Pin 8:** `D0`  
- **Pin 7:** `D1`  
- **Pin 6:** `D2`  
- **Pin 5:** `D3`  
- **Pin 4:** `D4`  
- **Pin 3:** `D5`  
- **Pin 2:** `D6`  
- **Pin 1:** `D7`  

**Control**

- **Pin 20:** `CS_BASIC1` / `CS_BASIC2` / `CS_BASIC3` / `CS_BASIC4` (per device)  
- **Pin 21:** `OE_ROM`  

**Power**

- **Pin 24:** `+5V`  
- **Pin 12:** `GND`  

---

### U13 — Monitor ROM

Same pinout as BASIC ROMs:

- **Pin 9–19:** `A0–A10`  
- **Pin 1–8:** `D7–D0`  
- **Pin 20:** `CS_MONITOR`  
- **Pin 21:** `OE_ROM`  
- **Pin 24:** `+5V`  
- **Pin 12:** `GND`  

---

### U14 — 6850 ACIA (DIP‑24)

**Data bus**

- **Pin 19:** `D0`  
- **Pin 18:** `D1`  
- **Pin 17:** `D2`  
- **Pin 16:** `D3`  
- **Pin 15:** `D4`  
- **Pin 14:** `D5`  
- **Pin 13:** `D6`  
- **Pin 12:** `D7`  

**Control / chip select / clock**

- **Pin 11:** `CS_ACIA`  
- **Pin 10:** `R_W`  
- **Pin 9:** `ACIA_CLK`  

**Serial I/O**

- **Pin 7:** `TX_DATA`  
- **Pin 6:** `RX_DATA`  
- **Pin 5:** `CTS`  
- **Pin 4:** `RTS`  

**Power**

- **Pin 24:** `+5V`  
- **Pin 1:** `GND`  

---

### U17 — 74LS139 (Dual 2‑to‑4 Decoder)

**Decoder A**

- **Pin 2:** `A0` (decode input)  
- **Pin 3:** `A1` (decode input)  
- **Pin 1:** `SEL_ROM_EN` (enable, local net)  
- **Pins 4,5,6,7:** `SEL_ROM0`, `SEL_ROM1`, `SEL_ROM2`, `SEL_ROM3` → feed `CS_BASICx` / `CS_MONITOR` via glue  

**Decoder B**

- **Pin 14:** `A0` (decode input)  
- **Pin 13:** `A1` (decode input)  
- **Pin 15:** `SEL_IO_EN` (enable, local net)  
- **Pins 12,11,10,9:** `SEL_IO0`, `SEL_IO1`, `SEL_IO2`, `SEL_IO3` → `SEL_RAM`, `SEL_IO`, `SEL_VIDEO`, etc.  

**Power**

- **Pin 16:** `+5V`  
- **Pin 8:** `GND`  

---

### U20, U22, U23 — 74LS138 (3‑to‑8 Decoders)

**Inputs**

- **Pin 1:** `A0` (decode input)  
- **Pin 2:** `A1`  
- **Pin 3:** `A2`  

**Enables**

- **Pin 6:** `G1` (active‑high enable, local net from glue)  
- **Pin 4:** `G2A` (active‑low enable)  
- **Pin 5:** `G2B` (active‑low enable)  

**Outputs (Y0–Y7)**

- **Pins 7–9, 10–12, 13–15:**  
  - Map to `CS_BASIC1`, `CS_BASIC2`, `CS_BASIC3`, `CS_BASIC4`, `CS_MONITOR`, `CS_RAMx`, `CS_IO`, `CS_VIDEO` as required per decoder instance.  

**Power**

- **Pin 16:** `+5V`  
- **Pin 8:** `GND`  

---

### Glue logic (U15, U16, U18, U19, U21)

Use local nets for intermediate decode:

- **NOR / NAND / inverter inputs:** address lines (`A13–A15`), `PHI2`, `R_W`, `RESET`, etc.  
- **Outputs:** `SEL_ROM`, `SEL_RAM`, `SEL_IO`, `SEL_VIDEO`, `RESET_N`, `WAIT` (if used).   

Connect all glue outputs to the appropriate enable pins on U17/U20/U22/U23 and to global nets where specified (`RESET_N` to counters, etc.).

---

## Sheet 2 — `RAM_BUS` (RAM, Bus Buffers, Additional Decode)

### U31–U40, U45–U52 — 2114 SRAM (DIP‑18)

**Address inputs**

- **Pin 9:** `A0`  
- **Pin 10:** `A1`  
- **Pin 11:** `A2`  
- **Pin 12:** `A3`  
- **Pin 13:** `A4`  
- **Pin 14:** `A5`  
- **Pin 15:** `A6`  

**Data I/O**

- **Pin 8:** `D0` / `BD0` (depending on whether buffered bus is used)  
- **Pin 7:** `D1` / `BD1`  
- **Pin 6:** `D2` / `BD2`  
- **Pin 5:** `D3` / `BD3`  

**Control**

- **Pin 16:** `CS_RAMx` (unique per device)  
- **Pin 3:** `RAM_WE_N`  
- **Pin 2:** `RAM_OE_N`  

**Power**

- **Pin 1:** `+5V`  
- **Pin 18:** `GND`  

---

### U24–U25 — 8T28 Bus Transceivers

**CPU data bus side**

- **Pins 2–9:** `D0`, `D1`, `D2`, `D3`, `D4`, `D5`, `D6`, `D7`  

**Buffered side**

- **Pins 11–18:** `BD0`, `BD1`, `BD2`, `BD3`, `BD4`, `BD5`, `BD6`, `BD7`  

**Control**

- **Pin 1:** `BUF_EN_DATA`  
- **Pin 19:** `BUF_DIR`  

**Power**

- **Pin 20:** `+5V`  
- **Pin 10:** `GND`  

---

### U2–U3 — 74LS75 Latches

- Connect latch inputs to address or control lines as per original decode (e.g., bank selects).  
- Outputs: `BK1`, `BK2`, or other bank‑select nets feeding `CS_RAMx` and buffer enables.  

---

### U4–U5 — 74LS125 Bus Buffers

- Inputs: selected address / data / control nets.  
- Outputs: buffered versions to RAM or I/O.  
- Enable pins: `BUF_EN_ADDR` or similar local nets.  

---

## Sheet 3 — `Keyboard_Logic`

### Keyboard matrix nets

**Rows**

- `KEY_ROW0–KEY_ROW7` — connect to row driver outputs (transistors / open‑collector gates) and diode matrix.  

**Columns**

- `KEY_COL0–KEY_COL9` — connect to diode matrix and to U42 parallel inputs.   

---

### U42 — 74LS165 (Parallel‑In Serial‑Out)

**Parallel inputs**

- **Pin 11:** `KEY_COL0`  
- **Pin 12:** `KEY_COL1`  
- **Pin 13:** `KEY_COL2`  
- **Pin 14:** `KEY_COL3`  
- **Pin 3:** `KEY_COL4`  
- **Pin 4:** `KEY_COL5`  
- **Pin 5:** `KEY_COL6`  
- **Pin 6:** `KEY_COL7`  

**Serial**

- **Pin 9:** `KEY_DATA_OUT`  

**Control**

- **Pin 2:** `KEY_CLK`  
- **Pin 1:** `KEY_LOAD_N`  

**Power**

- **Pin 16:** `+5V`  
- **Pin 8:** `GND`  

---

### U65, U69 — 74123 Monostables

For each device:

- **Pin 1:** `BREAK_KEY` or `KEY_ROWx` trigger (depending on function)  
- **Pin 2:** secondary trigger (local net)  
- **Pin 3:** `RESET` or `CLEAR` net (local)  
- **Pin 6:** `KEY_DEBOUNCE` or `BREAK_PULSE` (global/local as appropriate)  
- **Pin 14:** `+5V`  
- **Pin 7:** `GND`  

---

### U63 — 7474 D‑Flip‑Flop

- D, CLK, PRE, CLR: connect to `SHIFT_STATE`, `CTRL_STATE`, `KEY_DEBOUNCE`, etc.  
- Q/Q̅ outputs: `SHIFT_STATE`, `CTRL_STATE` nets.  

---

### U64 — 74LS76 JK Flip‑Flop

- J, K, CLK, CLR: connect to special key nets (`KEY_SHIFT_LOCK`, `KEY_CTRL`) and timing nets.  
- Outputs: `SHIFT_STATE`, `CTRL_STATE` or related state nets.  

---

### U70 — 7403 Open‑Collector NAND

- Inputs: `KEY_ROWx` / scan signals.  
- Outputs: row drive nets feeding diode matrix and/or `KEY_DRIVER` transistor bases.  

---

### Diodes D1–D10, D16–D20

- Anodes: `KEY_ROWx`  
- Cathodes: `KEY_COLx`  

---

### Transistors Q1, Q2

- Bases: `KEY_DRIVER` or `DAC_GATE` nets.  
- Collectors: row or DAC lines.  
- Emitters: `GND` or `+5V` depending on NPN/PNP role.  

---

## Sheet 4 — `Video_Timing`

### U41 — Character Generator ROM

**Address inputs**

- **Pins 9–?**: `ROW_ADDR0–ROW_ADDRn`  
- **Pins 10–?**: `COL_ADDR0–COL_ADDRm`  

**Data outputs**

- **Pins 1–8:** `CHAR_CODE0–CHAR_CODE7`  

**Control**

- **Pin 20:** `CS_CARGEN`  
- **Pin 21:** `OE_CARGEN`  

**Power**

- **Pin 24:** `+5V`  
- **Pin 12:** `GND`  

---

### U53–U55 — 74LS157 (Quad 2‑to‑1 Mux)

For each device:

- **Pins 2,5,11,14:** `A0–A3` (e.g., one video source)  
- **Pins 3,6,10,13:** `B0–B3` (alternate video source)  
- **Pin 1:** `VID_SEL`  
- **Pins 4,7,9,12:** `VID_DATA0–VID_DATA3` (or higher bits across devices)  
- **Pin 16:** `+5V`  
- **Pin 8:** `GND`  

---

### U30, U57, U59–U61 — 74LS163 Counters

For each counter:

- **Pin 2:** `DOT_CLK`  
- **Pin 1:** `RESET_N`  
- **Pin 9:** `LOAD` (local timing net)  
- **Pins 7,10:** `ENABLE` (local timing nets)  
- **Pins 11,12,13,14:** `H_COUNTx` or `V_COUNTx` (assign per device: horizontal vs vertical)  
- **Pin 16:** `+5V`  
- **Pin 8:** `GND`  

---

### U56 — 74LS20 (NAND)

- Inputs: selected `H_COUNTx`, `V_COUNTx` bits and timing nets.  
- Outputs: `HSYNC`, `VSYNC`, `COMP_SYNC` (or intermediate sync nets feeding U62).  

---

### U62 — 7404 Inverter

- Inputs: sync and video shaping nets (`HSYNC`, `VSYNC`, `VID_RAW`).  
- Outputs: conditioned sync/video nets (`VID_REF`, `COMP_SYNC`).  

---

### U66 — CA3130 Op‑Amp

- **Pin 3:** `VID_RAW`  
- **Pin 2:** `VID_REF`  
- **Pin 6:** `VIDEO_OUT`  
- **Pin 7:** `+5V`  
- **Pin 4:** `GND`  

Passives around U66:

- Resistors and caps form `VID_CLAMP`, gain/level networks; connect to `VID_RAW`, `VID_REF`, `VIDEO_OUT`, `GND`, `+5V` as per original schematic topology.   

---

## Sheet 5 — `Power_DAC_IO`

### Power entry

**D15 — 1N4001 Rectifier**

- **Anode:** `PWR_IN_RAW`  
- **Cathode:** `PWR_IN`  

**F1 — Fuse**

- **Input:** `PWR_IN`  
- **Output:** `+5V`  

Bulk caps:

- Connect between `+5V` and `GND` near power entry.  

---

### Reset / BREAK

- `RESET_IN` → external reset source / keyboard BREAK logic.  
- `RESET_OUT` → global `RESET` net (to CPU, counters, etc.).  
- `BREAK_KEY` → keyboard BREAK switch, feeds monostable (`BREAK_PULSE`) and reset gating.  

---

### DAC / Noise / Misc I/O

- `DAC_OUT` → DAC output node (to audio/noise circuitry).  
- `DAC_DISABLE` → control net to gate DAC / noise.  
- `NOISE` → noise source node.  
- `WKB` → original named net preserved (connect as per DAC/noise section).  

Transistors, resistors, caps:

- Connect around `DAC_OUT`, `DAC_DISABLE`, `NOISE`, `WKB` according to the original topology, with power rails `+5V` and `GND` and any coupling to I/O or speaker connector.

---

## Global Nets Summary

Use **global labels** for these across all sheets:

- `A0–A15`  
- `D0–D7`  
- `PHI2`  
- `R_W`  
- `RESET`, `RESET_N`  
- `IRQ`, `NMI`  
- `TX_DATA`, `RX_DATA`, `CTS`, `RTS`  
- `HSYNC`, `VSYNC`, `COMP_SYNC`, `VIDEO_OUT`  
- `KEY_ROW0–7`, `KEY_COL0–9`  
- `DAC_OUT`, `DAC_DISABLE`, `NOISE`, `WKB`  
- `+5V`, `GND`  

Use **local labels** for:

- `SEL_ROM`, `SEL_RAM`, `SEL_IO`, `SEL_VIDEO`  
- `CS_BASICx`, `CS_MONITOR`, `CS_RAMx`, `CS_ACIA`, `CS_CARGEN`  
- `BUF_EN_DATA`, `BUF_EN_ADDR`, `BK1`, `BK2`  
- `VID_RAW`, `VID_REF`, `VID_CLAMP`, `VID_SEL`  
- `KEY_DEBOUNCE`, `BREAK_PULSE`, `SHIFT_STATE`, `CTRL_STATE`  

This connection list should be enough for another Copilot (or you) to emit KiCad schematic text with zero guesswork.
