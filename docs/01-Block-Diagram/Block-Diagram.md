---
title: Individual Block Diagram
---

# Individual Block Diagram

## Overview

The individual block diagram documents the electrical design of the Liquid Amount Sensing subsystem for Fill-A-Bot. The subsystem uses a 1 kg load cell to measure the weight of the liquid. The small differential signal produced by the load cell is measured by a Nuvoton NAU7802KGI 24-bit sigma-delta ADC with a programmable gain amplifier.

A Microchip PIC18F57Q43 Curiosity Nano processes the weight measurement and interfaces with the rest of the Fill-A-Bot system using direct digital HIGH/LOW signals through TEAM_IN and TEAM_OUT.

The subsystem also includes local 5 V power regulation, a load-cell connector, ADC interface circuitry, a tare/zero pushbutton, status LED, GPIO expansion, and test points.


## Individual Block Diagram

![Fill-A-Bot Liquid Amount Sensing Individual Block Diagram](individual-block-diagram.png)

**Figure 1:** Individual block diagram for the Fill-A-Bot Liquid Amount Sensing subsystem.


## Power

The subsystem accepts a 9–12 V DC input through a 2-position screw-terminal connector. The input passes through a 500 mA fuse and fuse holder before reaching an LM7805CT linear voltage regulator.

The LM7805CT converts the input voltage to a regulated 5 V supply for the subsystem. A 0.33 µF capacitor is connected at the regulator input and a 0.1 µF capacitor is connected at the regulator output to help stabilize the regulator.

A local 5 V selection jumper connects the locally regulated supply to the +5V_BOARD rail used by the subsystem electronics.


## Liquid Amount Sensing

A Soldered Electronics 555026 / 100382 1 kg load cell is used to measure the combined weight of the container and liquid.

The load cell uses four electrical connections:

- **E+** — Positive bridge excitation
- **E-** — Negative bridge excitation
- **A+** — Positive differential output
- **A-** — Negative differential output

The load cell connects to the sensor PCB through an On Shore Technology OSTVN04A150 4-position load-cell connector.

The A+ and A- differential signals are routed to the NAU7802KGI through the analog input circuitry. Two 47 Ω series resistors and a 0.1 µF capacitor help filter noise from the low-level differential signal before analog-to-digital conversion.

The A+ and A- connections form a differential analog signal pair between the
load cell and the NAU7802. These two signal connections carry the low-level
millivolt output produced by the load cell.

## NAU7802 ADC Interface

The Nuvoton NAU7802KGI is a 24-bit sigma-delta ADC with a programmable gain amplifier. It amplifies and converts the small differential voltage produced by the load cell into digital measurement data that can be processed by the PIC18F57Q43.

The NAU7802 connects locally to the Curiosity Nano using three digital signals:

| **NAU7802 Signal** | **PIC18F57Q43 Pin** | **Purpose** |
| --- | --- | --- |
| SDIO | RB2 | Digital data and ADC configuration |
| SCLK | RB1 | Digital clock |
| DRDY | RC0 | Indicates when a new ADC conversion is ready |

The SDIO and SCLK lines use 4.7 kΩ pull-up resistors.

This ADC interface is local to the Liquid Amount Sensing subsystem and is separate from the direct digital communication used between the Fill-A-Bot subsystem boards.


## Team Communication

The Liquid Amount Sensing subsystem communicates with the Fill-A-Bot main controller using direct digital HIGH/LOW signals rather than UART or I2C.

The 8-position team connector uses the following connections:

| **Connector Pin** | **Signal** | **PIC Pin** | **Purpose** |
| --- | --- | --- | --- |
| Pin 1 | TEAM_IN | RA3 | Receives a digital HIGH/LOW state from the main controller |
| Pin 2 | TEAM_OUT | RA4 | Sends a digital HIGH/LOW state to the main controller |
| Pins 3–7 | NC | — | Unused by this subsystem |
| Pin 8 | GND | GND | Common ground between subsystem boards |

TEAM_IN allows the main controller to provide a control state to the Liquid Amount Sensing board.

TEAM_OUT allows the Liquid Amount Sensing board to provide a status state to the main controller, such as indicating that the desired weight condition has been reached.


## Tare / Zero Input

A momentary pushbutton is connected to PIC pin RA0 and is used as the TARE/ZERO input.

The input uses a 10 kΩ pull-up resistor. When the button is not pressed, the input is held HIGH. When the button is pressed, RA0 is connected to ground and becomes LOW.

The PIC can detect the button press and establish the current load-cell measurement as the zero or tare reference. This allows the empty container weight to be removed from subsequent liquid measurements.

A 1 µF capacitor is included to help filter and debounce the pushbutton signal.


## Status LED

A green status LED is controlled by PIC pin RC1 through a 1.2 kΩ current-limiting resistor.

The LED provides a visual indication that can be controlled by software to show subsystem status, measurement activity, tare completion, or debugging information.


## GPIO Expansion

A 6-pin expansion header provides four additional general-purpose I/O connections labeled GPIO1 through GPIO4.

The expansion header also provides +5V_BOARD and GND for connection to additional external hardware if required.


## Debugging and Test Points

Five test points are included on the subsystem PCB to provide convenient access to important power and ADC-related signals during subsystem testing and verification.

The status LED, tare/zero pushbutton, GPIO expansion header, and test points provide additional hardware access for testing and debugging without changing the normal operation of the Liquid Amount Sensing subsystem.
