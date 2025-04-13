# PD Trigger

**WIP. Don't try to reproduce it until it's complete!**


## Intro

[Schematics and PCBs](https://oshwlab.com/puzrin/project_koidnmat) on OSHWLab.

This project has two goals:

- Build development boards for writing [pdsink](https://github.com/pdsink/pdsink)
  drivers.
- Create a practical, advanced PD trigger.


Trigger features:

- Operation at voltages up to 48 V.
- Support for PPS profiles with current limiting, making it suitable for charging
  LiPo batteries (e.g., those used in power tools).
- Configuration via USB using a web app.
- Control via taps.

## Board compatibility

Some controllers are pin-to-pin compatible (but not at the software level).
The table below lists the development boards and their compatible chips.

| Board | Controllers | Package | Status |
|-------|-------------|---------|--------|
| fusb302 devboard | FUSB302BMPX, HUSB311BLA | WFQFN-14 | in progress |
| ch32x035 devboard | CH32X035F8U6 | QFN-20 | in progress |
| stm32g4 devboard | STM32G431KBU6 | LQFP-32 | in progress |
| tusb422 devboard | TUSB422IYFPR, RT1711HWSC, RT1715WSC, RT1716WSC | DSBGA / WL-CSP | in progress |


`ch32x035 lite` is a simplified trigger-only board:

- Minimal component count.
- No VBUS voltage measurement.
- No VBUS switch.

Expected use: when you just need a cheap, compact, yet advanced trigger.


## Notes

- External controllers are used with the `ESP32-S31-WROOM-3`. This module will
  be replaced with the `ESP32-S31-WROOM-1` when it becomes available.
- Almost all external chips DO NOT support VBUS voltages above 24-28 volts.
  Their VBUS inputs are clamped with a Zener diode and used only to detect
  "VBUS Present". That's acceptable for sink-only operation.
- On BGA chips, the central pin (INT_N) is routed through the unused VCONN pin
  to keep PCB requirements low. That's okay for sink-only devices.
