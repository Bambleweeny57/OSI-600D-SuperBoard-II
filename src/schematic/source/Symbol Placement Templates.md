# Ohio Scientific Superboard II – KiCad 10 Symbol Placement Templates
### Drop‑In Sheet Layouts (Builder‑Friendly)

Use these templates to place symbols on each hierarchical sheet in KiCad 10, in a logical left‑to‑right / top‑to‑bottom order that matches the original schematics.

---

## Sheet 1 – `CPU_ROM_ACIA`

### Recommended canvas layout

- **Top‑left:** CPU (U8)
- **Top‑right:** ACIA (U14)
- **Middle:** ROM block (U9–U13)
- **Bottom:** Decode logic (U15–U23)
- **Edges:** Power, reset, clock, connectors

### Symbol placement order

1. **U8 – 6502 CPU**
   - Library: `MCU`
   - Place centrally on the left.
2. **U14 – 6850 ACIA**
   - Library: `Interface_UART`
   - Place to the right of U8.
3. **U9–U12 – BASIC ROMs**
   - Library: `Memory_EPROM`
   - Place as a horizontal row under U8/U14.
4. **U13 – Monitor ROM**
   - Library: `Memory_EPROM`
   - Place next to U9–U12.
5. **U17 – 74LS139**
   - Library: `74xx`
   - Place below ROMs (start of decode).
6. **U20, U22, U23 – 74LS138**
   - Library: `74xx`
   - Place in a row under U17.
7. **U19 – 74LS20**
   - Library: `74xx`
   - Place under/near U17/U20 (glue logic).
8. **U15 – 74LS02**
   - Library: `74xx`
   - Place near U19 (NOR glue).
9. **U16, U18, U21 – 74LS04**
   - Library: `74xx`
   - Place around reset/clock nets (bottom‑left).
10. **Power & passives**
    - Decoupling caps near each IC (`Device:C_Small`)
    - Reset/clock resistors and caps (`Device:R`, `Device:C_Small`)
    - Diodes for reset/protection (`Device:D_Small`, `Device:D_Rectifier`)

---

## Sheet 2 – `RAM_BUS`

### Recommended canvas layout

- **Top:** Bus buffers / latches (U2–U7, U24–U25)
- **Middle:** RAM banks (U31–U40)
- **Bottom:** Extra RAM (U45–U52), bank select logic

### Symbol placement order

1. **U2–U3 – 74LS75**
   - Library: `74xx`
   - Place top‑left (latches).
2. **U4–U5 – 74LS125**
   - Library: `74xx`
   - Place top‑center (bus buffers).
3. **U6–U7 – 8T28**
   - Library: `74xx` (octal buffer)
   - Place top‑right (data bus transceivers).
4. **U24–U25 – 8T28**
   - Library: `74xx`
   - Place under U6–U7 (additional bus transceivers).
5. **U31–U40 – 2114 RAM**
   - Library: `Memory_RAM`
   - Place as a grid in the middle of the sheet (main RAM bank).
6. **U45–U52 – 2114 RAM**
   - Library: `Memory_RAM`
   - Place as a second grid below U31–U40 (extra RAM).
7. **Bank select / control nets**
   - Add labels `BK1`, `BK2`, `CS_RAMx`, `RAM_WE_N`, `RAM_OE_N`.
8. **Passives**
   - Decoupling caps near each RAM and buffer.
   - Pull‑ups/pull‑downs on bus/control lines (`Device:R`).

---

## Sheet 3 – `Keyboard_Logic`

### Recommended canvas layout

- **Left:** Keyboard matrix interface (rows/columns, diodes)
- **Center:** Shift register and timing logic
- **Right:** Flip‑flops, special key handling

### Symbol placement order

1. **Keyboard matrix nets**
   - Draw buses/labels: `KEY_ROW0–7`, `KEY_COL0–9`.
2. **Diodes – D1–D10, D16–D20**
   - Library: `Device:D_Small`
   - Place between row/column nets (matrix).
3. **U42 – 74LS165**
   - Library: `74xx`
   - Place center‑top (parallel‑in serial‑out).
4. **U65, U69 – 74123**
   - Library: `74xx`
   - Place center‑middle (debounce / BREAK timing).
5. **U63 – 7474**
   - Library: `74xx`
   - Place right‑top (SHIFT/CTRL state).
6. **U64 – 74LS76**
   - Library: `74xx`
   - Place right‑middle (additional state logic).
7. **U70 – 7403**
   - Library: `74xx`
   - Place near matrix/rows (open‑collector logic).
8. **Transistors – Q1, Q2**
   - Library: `Device:Q_NPN`, `Device:Q_PNP`
   - Place near DAC/keyboard control nets.
9. **Resistors**
   - Place around matrix, timing, and transistor stages (`Device:R`).

---

## Sheet 4 – `Video_Timing`

### Recommended canvas layout

- **Top:** Counters and timing (U30, U57, U59–U61)
- **Middle:** Character generator and muxes (U41, U53–U55)
- **Bottom:** Sync logic and analog video (U56, U62, U66)

### Symbol placement order

1. **U30, U57, U59–U61 – 74LS163**
   - Library: `74xx`
   - Place top‑left to top‑right (H/V counters).
2. **U41 – Character generator ROM**
   - Library: `Memory_ROM` / `Memory_EPROM`
   - Place middle‑left (char ROM).
3. **U53–U55 – 74LS157**
   - Library: `74xx`
   - Place middle‑center (video data mux).
4. **U56 – 74LS20**
   - Library: `74xx`
   - Place middle‑right (sync logic).
5. **U62 – 7404**
   - Library: `74xx`
   - Place near sync/video shaping nets.
6. **U66 – CA3130**
   - Library: `Analog_OpAmp`
   - Place bottom‑center (video output stage).
7. **Passives**
   - Timing caps (C6–C13, C57) around counters and sync.
   - Video path resistors and caps around U66 (`Device:R`, `Device:C_Small`).
   - Trimmers R57, R58 near video level/geometry (`Device:R_Potentiometer`).

---

## Sheet 5 – `Power_DAC_IO`

### Recommended canvas layout

- **Top‑left:** Power entry (rectifier, fuse, bulk caps)
- **Top‑right:** +5V distribution and decoupling
- **Bottom:** DAC, noise, BREAK/reset conditioning

### Symbol placement order

1. **D15 – 1N4001**
   - Library: `Device:D_Rectifier`
   - Place at power input.
2. **F1 – Fuse**
   - Library: `Device:Fuse`
   - Place after D15, feeding `+5V`.
3. **Bulk electrolytics – C‑506 series**
   - Library: `Device:CP_Electrolytic`
   - Place near power entry.
4. **Remaining bypass caps – CB‑10410**
   - Library: `Device:C_Small`
   - Place near analog/DAC and logic clusters.
5. **DAC / noise nets**
   - Add labels: `DAC_OUT`, `DAC_DISABLE`, `NOISE`, `WKB`.
6. **Transistors (if used here) – Q1, Q2**
   - Library: `Device:Q_NPN`, `Device:Q_PNP`
   - Place near DAC/noise circuitry.
7. **Resistors**
   - Place remaining R56–R62A, R72 etc. around DAC, noise, BREAK/reset (`Device:R`).

---

## General KiCad 10 Tips

- Create each sheet with the names above:  
  - `CPU_ROM_ACIA`, `RAM_BUS`, `Keyboard_Logic`, `Video_Timing`, `Power_DAC_IO`.
- Place symbols in the order listed, then:
  - Add **global labels** for cross‑sheet signals (buses, control, video, keyboard, DAC, power).
  - Add **local labels** for internal glue nets.
- Run ERC per sheet before updating the PCB.

---

If you want, I can now help you **sanity‑check one sheet at a time** as you build it in KiCad—starting with `CPU_ROM_ACIA`.
