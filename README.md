# esp32-i2c-net

An ESP32-S3 based I2C hub that distributes a buffered I2C bus over standard
6P6C (RJ12/RJ25) cables, so multiple remote I2C nodes can be wired back to a
single controller using cheap, keyed telephone-style patch cords. The use of
I2C bus driver allow the connection of multiple sensor over long wires.

## Hardware

- **MCU:** ESP32-S3-WROOM-1 (U1)
- **I2C buffering:** PCA9517 level-shifting I2C repeater (U4) plus an
  LTC4311 active rise-time accelerator (U3) to keep edges clean over long
  cable runs
- **Bus ports:** 4× 6P6C modular jacks (J3–J6)
- **USB:** USB-A connector (J1) wired to the ESP32-S3 native USB pins
  (GPIO19 = D−, GPIO20 = D+) for connection of an optional USB device, like a camera.
- **Power:** +5 V input via barrel jack (J2) or USB; AMS1117-3.3 LDO (U2)
  provides the +3.3 V rail
- **Indicators / misc:** WS2812B addressable RGB LED (D1, data on GPIO38),
  reset pushbutton (SW1 on EN), 3.3 V test point (TP1), auxiliary 1×6 header
  (J7) exposing spare GPIOs

### 6P6C port pinout (J3–J6)

| Pin | Signal     |
|-----|------------|
| 1   | GND        |
| 2   | SDA        |
| 3   | +5 V       |
| 4   | +5 V       |
| 5   | SCL        |
| 6   | GND        |
| SH  | Shield/GND |

The buffered bus on the jacks runs at 5 V logic levels (PCA9517 A-side at
+5 V with pull-ups R4/R5); the ESP32 side of the repeater runs at 3.3 V
(GPIO1 = SDA, GPIO2 = SCL, pull-ups R1/R2/R3). The PCA9517 also isolates
the cable capacitance from the MCU bus.

## Repository contents

| File                    | Description                                  |
|-------------------------|----------------------------------------------|
| `esp32-i2c-net.kicad_pro`  | KiCad 7 project file                      |
| `esp32-i2c-net.kicad_sch`  | Schematic                                 |
| `esp32-i2c-net.kicad_pcb`  | PCB layout                                |

## Requirements

- KiCad 7 or later (files use the KiCad 7 schematic/PCB format)

## Status

Work in progress — schematic complete, PCB layout in progress
(DSN exports for the Freerouting autorouter are included).
No firmware in this repository.

## License

No license file is currently included; the design files are provided as-is.
