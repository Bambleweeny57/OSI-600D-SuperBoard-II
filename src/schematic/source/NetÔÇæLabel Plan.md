# Ohio Scientific Superboard II – KiCad 10 Net‑Label Plan
### Sheet‑by‑Sheet Wiring Guide (Zero Ambiguity)

This document defines the net labels to use when rebuilding the Superboard II schematic in KiCad 10.  
Labels follow the original schematics wherever possible and introduce consistent prefixes for clarity.

---

## Sheet 1 — CPU, ROM, ACIA, Core Decode

### Address Bus
- `A0`
- `A1`
- `A2`
- `A3`
- `A4`
- `A5`
- `A6`
- `A7`
- `A8`
- `A9`
- `A10`
- `A11`
- `A12`
- `A13`
- `A14`
- `A15`

### Data Bus
- `D0`
- `D1`
- `D2`
- `D3`
- `D4`
- `D5`
- `D6`
- `D7`

### CPU Control
- `PHI2` (or `Φ2`)
- `R_W` (or `R/W`)
- `RESET`
- `IRQ`
- `NMI`
- `VMA` (if present)

### ROM Chip Selects
- `CS_BASIC1`
- `CS_BASIC2`
- `CS_BASIC3`
- `CS_BASIC4`
- `CS_MONITOR`

Use `_N` suffix if you prefer explicit active‑low notation (e.g., `CS_BASIC1_N`).

### ACIA (6850) Signals
- `CS_ACIA`
- `ACIA_CLK` (or `BRG`)
- `TX_DATA`
- `RX_DATA`
- `CTS`
- `RTS`

### Decode Logic Nets
- `SEL_ROM`
- `SEL_RAM`
- `SEL_IO`
- `SEL_VIDEO`
- `RESET_N` (if inverted)
- `WAIT` (if present)

---

## Sheet 2 — RAM, Bus Buffers, Additional Decode

### Address Bus
Same labels as Sheet 1:
- `A0` … `A15`

### Data Bus
Same labels as Sheet 1:
- `D0` … `D7`

### Buffered Data Bus (if used)
- `BD0`
- `BD1`
- `BD2`
- `BD3`
- `BD4`
- `BD5`
- `BD6`
- `BD7`

### RAM Control
- `CS_RAM0`  
- `CS_RAM1`  
- `CS_RAM2`  
- … (continue for all 2114 devices)
- `RAM_WE_N`
- `RAM_OE_N`

### Bank Selects (if present)
- `BK1`
- `BK2`

### Buffer / Latch Control
- `BUF_EN_DATA`
- `BUF_EN_ADDR`
- `LATCH_OUTx` (if used)

---

## Sheet 3 — Keyboard Logic & Interface

### Keyboard Matrix
**Rows:**
- `KEY_ROW0`
- `KEY_ROW1`
- `KEY_ROW2`
- `KEY_ROW3`
- `KEY_ROW4`
- `KEY_ROW5`
- `KEY_ROW6`
- `KEY_ROW7`

**Columns:**
- `KEY_COL0`
- `KEY_COL1`
- `KEY_COL2`
- `KEY_COL3`
- `KEY_COL4`
- `KEY_COL5`
- `KEY_COL6`
- `KEY_COL7`
- `KEY_COL8`
- `KEY_COL9`

### Special Keys
- `KEY_BREAK`
- `KEY_SHIFT_LOCK`
- `KEY_CTRL`
- `KEY_RETURN`
- `KEY_SPACE`

### Shift Register (74LS165)
- `KEY_DATA_OUT`
- `KEY_CLK`
- `KEY_LOAD_N`

### Timing / Debounce
- `KEY_DEBOUNCE`
- `BREAK_PULSE`
- `SHIFT_STATE`
- `CTRL_STATE`

### Discretes
- Diodes: keep refdes (`D1–D20`) but label nets as `KEY_ROWx` / `KEY_COLx`
- Transistors:
  - `KEY_DRIVER`
  - `DAC_GATE` (if used)

---

## Sheet 4 — Video Generation & Timing

### Character & Video Data
- `CHAR_CODE0` … `CHAR_CODE7`
- `VID_DATA0` … `VID_DATA7`

### Addressing for Character ROM
- `ROW_ADDR0` … `ROW_ADDRn`
- `COL_ADDR0` … `COL_ADDRm`

### Counters (74LS163)
- `H_COUNT0` … `H_COUNTn`
- `V_COUNT0` … `V_COUNTn`

### Clocks
- `DOT_CLK`
- `VID_CLK`

### Sync Logic
- `HSYNC`
- `VSYNC`
- `COMP_SYNC`

### Video Output Path
- `VID_RAW`
- `VID_REF`
- `VID_CLAMP`
- `VIDEO_OUT`

---

## Sheet 5 — Power, DAC, Misc I/O

### Power Nets
- `+5V`
- `GND`
- `PWR_IN`
- `PWR_IN_RAW` (rectifier input)

### Reset / BREAK
- `RESET`
- `BREAK_KEY`
- `RESET_IN`
- `RESET_OUT`

### DAC / Noise
- `DAC_OUT`
- `DAC_DISABLE`
- `NOISE`
- `WKB` (keep original name)

### Protection
- Fuse F1: `PWR_IN` → `+5V`
- Rectifier D15: `PWR_IN_RAW` → `PWR_IN`

---

## Global Label Rules

### Use **global labels** for:
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

### Use **local labels** for:
- Intermediate decode nets (`SEL_ROM`, `SEL_RAM`, etc.)
- Internal video nets (`VID_RAW`, `VID_REF`, etc.)
- Keyboard timing nets (`KEY_DEBOUNCE`, `BREAK_PULSE`)
- Buffer/latch control (`BUF_EN_DATA`, `LATCH_OUTx`)

---

## Notes
- When the original schematic prints a name, **use it exactly**.  
- When a signal is active‑low, you may suffix `_N` for clarity.  
- Keep buses consistent across sheets to avoid ERC/DRC confusion.

---

## Optional Next Step
If you want, I can generate a **pin‑by‑pin wiring map** for Sheet 1 (CPU + ROM + ACIA + decode), so you can wire that sheet with absolutely no guesswork.
