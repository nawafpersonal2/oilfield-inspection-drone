# Oilfield Inspection Drone

An FPV quadcopter built around **a flight controller I designed from scratch** — the SOWA F4 — carrying a gas sensor and a temperature sensor to inspect oil field installations and detect gas leaks or abnormal heat before they become incidents.

Everything except the off-the-shelf motors, ESC and radio gear was designed for this project: the flight controller PCB, the 3D printed airframe pod, and the sensor mounts.

![Assembled drone](media/images/hero.jpg)

*[العربية](README.ar.md)*

---

## Why

Inspecting pipelines, flanges, valves and storage tanks in an oil field usually means sending a person into a hot, remote and potentially hazardous area. A small drone can fly the same route in minutes, stream live video to the pilot, and read gas concentration and surface temperature at the same time — nobody has to stand next to a possible leak.

## The Flight Controller — SOWA F4 v1.0

The core of this project. A 4-layer 30.5×30.5 mm flight controller designed in EasyEDA, built around the STM32F405 and fully compatible with Betaflight.

![SOWA F4 board](media/images/pcb-3d.png)

| Block | Part | Purpose |
|---|---|---|
| MCU | STM32F405RGT6 | Main processor, 168 MHz |
| IMU | ICM-42688-P | Gyro + accelerometer, SPI |
| Barometer | DPS310 | Altitude hold |
| Blackbox | W25Q128 (16 MB) | Flight log storage |
| OSD | AT7456E + 27 MHz crystal | Overlays telemetry on the video feed |
| 5V rail | LMR16030 buck, 3.5 A | Peripherals, receiver, camera |
| 10V rail | LMR16030 buck, 3.5 A | VTX supply |
| 3.3V rail | AMS1117-3.3 | Logic |
| Input range | 7–36 V (2S–8S) | With reverse polarity protection |
| USB | Type-C | Configuration and flashing |
| UARTs | 6 exposed | RX, VTX, GPS, telemetry |
| ESC | 8-pin JHEMCU-standard connector | 4-in-1 ESC, S1–S4 + current sense |

The board also includes a hardware SBUS inverter, VBAT voltage divider for battery monitoring, a beeper driver, and an addressable LED output.

**Full schematic:**

![Schematic](media/images/schematic.png)

Source files, Gerbers and BOM are in [`hardware/pcb/`](hardware/pcb/).

## Wiring

How the board connects to the rest of the aircraft:

![Wiring diagram](media/images/wiring-diagram.png)

## Airframe

The pod, canopy, sensor tower and bottom plate were modelled in Fusion 360 and printed on a Creality Ender 3 S1. The design places the gas sensor on top of the airframe, above and clear of the propeller wash, so it samples the surrounding air rather than the air the props are pushing down.

<!-- TODO: material and print settings, e.g. PETG, 0.2 mm layer, 4 walls, 30% infill -->

| CAD | Exploded parts |
|---|---|
| ![CAD](media/images/frame-cad.jpg) | ![Parts](media/images/frame-parts.png) |

Printing in progress:

![Printing](media/images/printing.png)

STL and Fusion source files are in [`hardware/frame/`](hardware/frame/).

## Sensors

![Top view showing the gas sensor](media/images/drone-top.jpg)

| Sensor | Part | Reads |
|---|---|---|
| Gas | MQ-series <!-- TODO: exact model, e.g. MQ-2 / MQ-5 --> | Combustible gas / hydrocarbon vapour, analog |
| Temperature | <!-- TODO: model --> | <!-- TODO: contact or IR non-contact? --> |

<!-- TODO: how the readings reach the pilot — OSD overlay, telemetry, or logged onboard? -->

## Remaining Hardware

| Subsystem | Part |
|---|---|
| Motors | <!-- TODO: e.g. 2207 1750KV --> |
| ESC | 4-in-1, <!-- TODO: current rating --> |
| Propellers | 5" tri-blade |
| FPV camera | <!-- TODO: model --> |
| VTX | 5.8 GHz, <!-- TODO: power --> |
| Radio link | <!-- TODO: ELRS / Crossfire --> |
| Goggles | <!-- TODO: model --> |
| Battery | <!-- TODO: e.g. 4S 1500 mAh LiPo --> |

## Software

Flight control runs on **Betaflight**. The full configuration is exported as a CLI dump so the exact setup can be reproduced:

```bash
# Betaflight Configurator → CLI tab
diff all        # inspect current config
# to restore this build's config, paste the contents of:
# firmware/betaflight/cli_dump.txt
```

## Repository Structure

```
.
├── hardware/
│   ├── pcb/          # EasyEDA source, schematic, Gerbers, BOM
│   └── frame/        # Fusion 360 source + STL files
├── firmware/
│   └── betaflight/   # CLI dump, tuning notes
├── docs/
│   └── assembly.md   # build notes
├── media/
│   └── images/
└── README.md
```

## Safety

- LiPo batteries: charge in a fire-safe bag, never unattended, never fly a puffed pack.
- Props off whenever the battery is connected on the bench.
- **This aircraft is not certified for hazardous or explosive atmospheres.** Heated-element gas sensors, brushless motors and LiPo packs are all ignition sources. Treat it as a prototype and research platform — real deployment near live hydrocarbon leaks requires intrinsically safe (ATEX / IECEx) rated equipment.
- Follow local UAV regulations — in Saudi Arabia, GACA registration and airspace rules — and get site permission before flying over any facility.

## Roadmap

- [ ] Gas and temperature readings overlaid on the FPV feed via the onboard OSD
- [ ] Timestamped data logging to the onboard flash
- [ ] GPS and waypoint missions for repeatable inspection routes
- [ ] Sensor calibration against a reference gas concentration
- [ ] v1.1 board revision <!-- TODO: any fixes found after assembling v1.0? -->

## License

<!-- TODO: MIT for firmware, CERN-OHL-S for the hardware is a common pairing -->

## Author

Nawaf Alghamdi <!-- TODO: LinkedIn / contact -->
