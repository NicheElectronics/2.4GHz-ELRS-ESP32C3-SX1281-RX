# 2.4 GHz ExpressLRS Receiver | ESP32-C3 + SX1281

A compact **20 mm × 15 mm** 2.4 GHz ExpressLRS receiver designed around an **ESP32-C3** microcontroller and **SX1281** RF transceiver. The board provides power and a UART connection to a flight controller.

> **Status:** The custom PCB was assembled, flashed and brought up, and receiver operation was tested on a drone. No range, latency or RF-compliance measurements are claimed here.

## Hardware

| Item | Implementation |
| --- | --- |
| MCU | ESP32-C3 |
| RF transceiver | SX1281, 2.4 GHz |
| Interface to flight controller | UART |
| Board size | 20 mm × 15 mm |
| Design tool | EasyEDA |
| PCB | Six layers |

The recorded layer order is **top / GND / 3.3 V / 3.3 V / GND / bottom**. Check the board revision's design files before ordering or modifying the PCB.

## Signal path

```mermaid
flowchart LR
    RADIO["ExpressLRS transmitter"] <-->|"2.4 GHz RF"| SX["SX1281"]
    SX <-->|"SPI"| ESP["ESP32-C3"]
    ESP <-->|"UART"| FC["Flight controller"]
```

The RF link terminates at the SX1281; the ESP32-C3 runs the receiver firmware and communicates with the flight controller over UART. Check the schematic for the exact voltage, pads and pin assignments before wiring the board.

## Firmware and bring-up

The tested receiver configuration used **ExpressLRS 4.1.0** with the **Generic ESP32-C3 2.4 GHz RX / `UNIFIED_ESP32C3_2400_RX`** target and SX128X radio family, as shown in the project's configuration evidence. The firmware artifacts previously prepared for this board include `AIRWINGS-ELRS-RX-4.1.0.bin` and `Generic-C3-2400-RX.json`; use the configuration matching your hardware revision.

For a new build or reflash:

1. Confirm the board's power, UART wiring, boot method and RF antenna connection from the schematic.
2. Select the correct ExpressLRS receiver target and board configuration. Follow the [official ExpressLRS documentation](https://www.expresslrs.org/) for the flashing method supported by that firmware version.
3. Check that the receiver starts, shows the expected device/target information and binds to a compatible transmitter.
4. Connect the UART to a flight-controller UART, configure the matching serial receiver protocol in the flight-controller software, and verify channel movement before flight.

The **same physical PCB** was also reconfigured and flashed for transmitter/telemetry experiments. This was a firmware/configuration reuse of the receiver hardware, not a redesigned telemetry PCB. Receiver operation on the drone does not by itself establish validated transmitter performance.

## Test status

- Custom board assembled and powered up.
- ExpressLRS firmware flashed and receiver configuration checked.
- Receiver function tested with a drone installation.

Detailed RF range, sensitivity, packet-loss and compliance figures have not been provided. Add reproducible measurements and test conditions if those are evaluated later.

## Author

**Nishant Patil**

No license has been specified for the project files. Add one if you want to define reuse terms.
