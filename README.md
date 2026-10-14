# esp32-weather-station

ESP32-based weather station with a BME280 sensor and a 16x2 LCD display.
It measures temperature, humidity and pressure, shows them on the LCD and serves them over Wi-Fi through a small web server running on the ESP32.

<!-- Add a photo of the assembled station here -->
<!-- ![Weather station](images/station.jpg) -->

## Features

- Temperature, humidity and pressure from a BME280 (I²C)
- 16x2 LCD driven in 4-bit parallel mode, contrast set by a potentiometer
- Web page with the current readings, served by the ESP32 over Wi-Fi
- Runs on 3×AA batteries with a power switch
- 3D-printed enclosure designed in FreeCAD

## Hardware

| Part | Notes |
|---|---|
| ESP32 DevKit V1 (30-pin, ESP32-WROOM-32) | micro-USB |
| BME280 module | 4-pin I²C (VIN, GND, SCL, SDA) |
| LCD 1602 (HD44780-compatible) | 4-bit mode, R/W tied to GND |
| 10 kΩ potentiometer | LCD contrast |
| Switch | in series with battery + |
| 3×AA battery holder | ~4.5 V into VIN |

## Wiring

| From | To (ESP32) |
|---|---|
| BME280 SDA | GPIO21 |
| BME280 SCL | GPIO22 |
| BME280 VIN | 3V3 |
| LCD RS | GPIO19 |
| LCD E | GPIO23 |
| LCD D4 | GPIO18 |
| LCD D5 | GPIO17 |
| LCD D6 | GPIO16 |
| LCD D7 | GPIO4 |
| LCD V0 | potentiometer wiper |
| LCD VDD, A | battery + (after switch) |
| LCD VSS, R/W, K | GND |
| Battery + (after switch) | VIN |

All grounds are common. The full schematic is in [`hardware/pcb`](hardware/pcb).

## Enclosure

The enclosure is designed in FreeCAD as a two-part case joined with snap-fits, so it can be printed and assembled without screws.

- **v1:** printed in PLA, screw-mounted. It needed several screw sizes, and I forgot the power switch and an anti-rotation tab for the potentiometer.
- **v2:** screwless snap-fit case, raised battery compartment with the ESP32 underneath, power switch added. Designed, not printed yet.

Files: [`hardware/enclosure`](hardware/enclosure)

## PCB (in progress)

A carrier board designed in KiCad that replaces the jumper wires. The ESP32 DevKit, BME280 module and LCD plug into headers on the board.

- [x] Schematic
- [ ] Footprints and layout
- [ ] Order and assemble
- [ ] Fit the enclosure to the board

Files: [`hardware/pcb`](hardware/pcb)

## Building the firmware

1. Install the ESP32 board package in the Arduino IDE.
2. Install the libraries: <!-- list the libraries you actually use, e.g. Adafruit BME280, LiquidCrystal -->
3. Set your Wi-Fi name and password in the sketch.
4. Select **ESP32 Dev Module** (or **DOIT ESP32 DEVKIT V1**) and upload.
5. Open the Serial Monitor to see the IP address, then open it in a browser.

## Repository structure

```
firmware/            Arduino sketch
hardware/enclosure/  FreeCAD files, STL/3MF for printing
hardware/pcb/        KiCad project and schematic PDF
images/              Photos
```

## Next steps

- Finish and order the carrier PCB
- Move the firmware from Arduino to ESP-IDF with FreeRTOS tasks
- Publish readings over MQTT
