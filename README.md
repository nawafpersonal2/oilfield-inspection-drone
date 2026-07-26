# FPV Inspection Drone — Gas Leak & Thermal Detection for Oil Fields

A custom-built FPV quadcopter carrying a gas sensor and a temperature sensor, designed to inspect oil field installations and detect gas leaks or abnormal heat before they become incidents. The frame is 3D printed and the sensor board is a custom PCB designed for this project.

<!-- TODO: replace with your best hero photo -->
![Assembled drone](media/images/hero.jpg)

*[العربية](README.ar.md)*

---

## Why

Inspecting pipelines, flanges, valves and storage tanks in an oil field usually means sending a person into a hot, remote, and potentially hazardous area. A small drone can fly the same route in minutes, stream live video to the pilot, and read gas concentration and surface temperature at the same time — no one has to stand next to a possible leak.

## Features

- Live FPV video to head-mounted goggles for close-range manual inspection
- Gas sensing for combustible gas / hydrocarbon vapor detection
- Temperature sensing to spot overheating equipment
- Custom PCB carrying the sensors and their interface to the flight stack
- Fully 3D printed frame and sensor mounts, designed around the electronics
- Betaflight-based flight control, tuned for stable low-speed inspection flight

## Hardware

| Subsystem | Part | Notes |
|---|---|---|
| Flight controller | STM32 **F405** FC | Runs Betaflight |
| Motor control | 4-in-1 **ESC** | <!-- TODO: current rating, e.g. 45A --> |
| Motors | <!-- TODO: e.g. 2306 1700KV --> | |
| Propellers | <!-- TODO: size/pitch --> | |
| Video transmitter | **VTX** | <!-- TODO: 5.8 GHz, power output --> |
| FPV camera | <!-- TODO: model --> | |
| Goggles | <!-- TODO: model --> | Head-mounted, pilot view |
| Radio link | Receiver + transmitter | <!-- TODO: protocol, e.g. ELRS / CRSF --> |
| Gas sensor | <!-- TODO: e.g. MQ-2 / MQ-5 / MQ-135 --> | Analog output |
| Temperature sensor | <!-- TODO: e.g. MLX90614 IR / DS18B20 --> | <!-- contact or non-contact? --> |
| Sensor board | Custom PCB (see `hardware/pcb/`) | Designed in <!-- TODO: KiCad / EasyEDA / Altium --> |
| Frame | 3D printed (see `hardware/frame/`) | <!-- TODO: material, e.g. PETG / ASA --> |
| Battery | <!-- TODO: e.g. 4S 1500mAh LiPo --> | |

### Custom PCB

<!-- TODO: 1–2 paragraphs: what the board does, power rails, how sensor data reaches the pilot -->

![PCB](media/images/pcb.jpg)

Source files, schematic, and Gerbers are in [`hardware/pcb/`](hardware/pcb/).

### 3D Printed Frame

<!-- TODO: design intent — arm length, weight, sensor placement away from motor wash, print settings -->

![Frame](media/images/frame.jpg)

STL and source CAD files are in [`hardware/frame/`](hardware/frame/).

## Software

Flight control runs on **Betaflight**. The full configuration is exported as a CLI dump so anyone can reproduce the exact setup:

```bash
# In Betaflight Configurator → CLI tab
diff all        # inspect current config
# to restore this build's config, paste the contents of:
# firmware/betaflight/cli_dump.txt
```

<!-- TODO: if the sensors run their own microcontroller firmware, describe it here and put the code in firmware/sensors/ -->

## Repository Structure

```
.
├── hardware/
│   ├── pcb/          # schematic, layout, Gerbers, BOM
│   └── frame/        # CAD source + STL files for printing
├── firmware/
│   ├── betaflight/   # CLI dump, tuning notes
│   └── sensors/      # sensor board firmware
├── docs/
│   ├── wiring.md     # wiring diagram and pin mapping
│   └── assembly.md   # build steps
├── media/
│   ├── images/
│   └── videos/
└── README.md
```

## Gallery

<!-- TODO: add your photos here. For videos, see the note below. -->

| | |
|---|---|
| ![](media/images/build-1.jpg) | ![](media/images/build-2.jpg) |
| ![](media/images/field-test-1.jpg) | ![](media/images/field-test-2.jpg) |

**Flight footage:** <!-- TODO: YouTube link — GitHub caps files at 100 MB, so host video externally and link it -->

## Safety

- LiPo batteries: charge in a fire-safe bag, never charge unattended, never fly a puffed pack.
- Props off whenever the battery is connected on the bench.
- **This drone is not certified for hazardous/explosive atmospheres.** Heated-element gas sensors, brushless motors, and LiPo packs are all ignition sources. Treat it as a prototype and research platform — real deployment near live hydrocarbon leaks needs intrinsically safe (ATEX / IECEx) rated equipment.
- Follow local UAV regulations (in Saudi Arabia, GACA registration and airspace rules) and get site permission before flying over any facility.

## Roadmap

- [ ] Telemetry overlay of gas/temperature readings on the FPV feed (OSD)
- [ ] Data logging to onboard storage with timestamps
- [ ] GPS + waypoint mission for repeatable inspection routes
- [ ] Sensor calibration against a reference gas concentration
- [ ] Enclosure sealing for dust and heat

## License

<!-- TODO: pick one — MIT for code, CERN-OHL-S for hardware, CC-BY-SA for docs is a common combo -->

## Author

<!-- TODO: your name, LinkedIn, contact -->
