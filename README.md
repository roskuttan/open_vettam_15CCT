# open_vettam_15CCT

Tunable-white ceiling-light hardware project with a main control board and a
separate circular LED MCPCB.

## Current Hardware

### LED MCPCB

Verified from the current KiCad schematic and PCB:

- 130 mm circular board routed on `F.Cu`.
- 84 LEDs: 42 x `L128-5090HA35000K1` cool-white 5000 K and
  42 x `L128-3090HA35000K1` warm-white 3000 K.
- Six CW strings and six WW strings, each with a `6.8 ohm` resistor.
- LED power pads are `CW+`, `WW+`, and one shared `LED-`.
- The shared `LED-` pad connects to `GND0` used by both LED sheets.
- The three LED power wire pads are `3 x 6 mm`. The previous four separate
  power pads were `5 x 10 mm`.
- A `TMP112AIDRLR` temperature sensor is connected through `TEMP_3V3`,
  `TEMP_GND`, `TEMP_SCL`, and `TEMP_SDA` pads.

Sources:

- [`hardware/led-mcpcb/kicad/led_mcpcb.kicad_sch`](hardware/led-mcpcb/kicad/led_mcpcb.kicad_sch)
- [`hardware/led-mcpcb/kicad/led_mcpcb.kicad_pcb`](hardware/led-mcpcb/kicad/led_mcpcb.kicad_pcb)
- [`hardware/led-mcpcb/kicad/CW-5000.kicad_sch`](hardware/led-mcpcb/kicad/CW-5000.kicad_sch)
- [`hardware/led-mcpcb/kicad/WW-3000.kicad_sch`](hardware/led-mcpcb/kicad/WW-3000.kicad_sch)

### Main Board

Verified from the current KiCad schematic and PCB:

- 68.25 x 49 mm, two copper layers, fully routed.
- `24V` input with an `LMR51610YDBVR` buck regulator producing `3V3`.
- `ESP32-C6-MINI-1-N4` controller module.
- Two `TPS922053DRRR` LED drivers controlled by `PWM_CW` and `PWM_WW`.
- `LED_OUT` connector `J3` pinout:

| Pin | Current net |
|---:|---|
| 1 | `+24V` |
| 2 | `WW-` |
| 3 | `+24V` |
| 4 | `CW-` |

- `TEMP_IN` connector `J5` pinout:

| Pin | Current net |
|---:|---|
| 1 | `+3V3` |
| 2 | `GND` |
| 3 | `SCL` |
| 4 | `SDA` |

Sources:

- [`hardware/main-board/kicad/open_vettam_15CCT.kicad_sch`](hardware/main-board/kicad/open_vettam_15CCT.kicad_sch)
- [`hardware/main-board/kicad/open_vettam_15CCT.kicad_pcb`](hardware/main-board/kicad/open_vettam_15CCT.kicad_pcb)
- [`hardware/main-board/kicad/24v_Input.kicad_sch`](hardware/main-board/kicad/24v_Input.kicad_sch)
- [`hardware/main-board/kicad/24-5_buck.kicad_sch`](hardware/main-board/kicad/24-5_buck.kicad_sch)
- [`hardware/main-board/kicad/MCU.kicad_sch`](hardware/main-board/kicad/MCU.kicad_sch)
- [`hardware/main-board/kicad/cc_driver.kicad_sch`](hardware/main-board/kicad/cc_driver.kicad_sch)

## Interface Status

The current board files do not have matching LED power interfaces:

- The LED MCPCB uses `CW+`, `WW+`, and shared `LED-`.
- The main board still outputs `+24V`, `WW-`, `+24V`, and `CW-`.

The main-board LED-driver section must be revised before it can connect directly
to the current LED MCPCB interface.

## Repository Layout

```text
hardware/
  main-board/
    kicad/          Main-board KiCad source
    bom/            Main-board BOM export
    manufacturing/  Gerber ZIP, netlist, and stencil DXF files
  led-mcpcb/
    kicad/          LED-board KiCad source
    manufacturing/  LED-board stencil DXF
firmware/
  esp32-c6/         Firmware placeholder; no source code is present yet
docs/               Datasheets and manufacturing notes
cad/                Enclosure CAD
mechanical/         Mechanical models and assembly assets
```

Matter over Thread, CW/WW PWM, brightness control, and color-temperature control
are listed as planned firmware scope in
[`firmware/esp32-c6/README.md`](firmware/esp32-c6/README.md); they are not
implemented in this repository yet.

## License

- Hardware and CAD source: CERN-OHL-P-2.0
- Firmware and scripts: MIT
- Documentation and media: not licensed unless stated otherwise

See [`LICENSE`](LICENSE) and [`LICENSES/`](LICENSES/).
