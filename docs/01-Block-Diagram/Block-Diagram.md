---
title: Individual Block Diagram
---

## Overview

The individual block diagram documents the electrical design of the Liquid Amount Sensing subsystem for Fill-A-Bot. The subsystem measures the amount of liquid using a 1 kg load cell connected to a Nuvoton NAU7802 24-bit load-cell ADC. A PIC18F57Q43 Curiosity Nano reads the NAU7802 using I2C and communicates with the Fill-A-Bot system using UART.

The subsystem includes its own 5 V power regulation, load-cell interface, ADC circuitry, team communication interface, GPIO expansion, debugging circuitry, and test points.

## Individual Block Diagram

![Fill-A-Bot Liquid Amount Sensing Individual Block Diagram](individual-block-diagram.png)

**Figure 1:** Individual block diagram for the Fill-A-Bot Liquid Amount Sensing subsystem.

## Power

The subsystem accepts a 9–12 V DC input through a 2-position screw-terminal connector. The input passes through a 500 mA fuse before reaching an LM7805CT linear voltage regulator.

The LM7805CT converts the input voltage to a regulated 5 V supply for the subsystem. A 0.33 µF capacitor is connected at the regulator input and a 0.1 µF capacitor is connected at the regulator output.

A local 5 V selection jumper is included between the locally regulated supply and the +5V_BOARD rail.

## Liquid Amount Sensing

A 1 kg Soldered Electronics 555026 load cell is used to measure the weight of the liquid. The load cell connects to the sensor board through four connections: A+, A−, E+, and E−.

The differential output from the load cell is connected to a Nuvoton NAU7802 24-bit load-cell ADC. The analog input includes two 47 Ω resistors and filtering to condition the low-level differential signal before conversion.

The NAU7802 communicates with the PIC18F57Q43 Curiosity Nano using I2C. SDA and SCL use 4.7 kΩ pull-up resistors. The NAU7802 DRDY signal is also connected to the Curiosity Nano to indicate when a new ADC conversion is available.

## Team Communication

The Liquid Amount Sensing subsystem communicates with the Fill-A-Bot system using UART through the 8-pin team connector.

The team UART transmit signal is connected to the UART receive input of the Curiosity Nano, and the Curiosity Nano UART transmit output is connected to the team UART receive signal.

The connector also provides a common ground connection. Unused connector positions are left unconnected.

## GPIO Expansion

A 6-pin expansion header provides four general-purpose I/O signals labeled GPIO1 through GPIO4. The header also provides +5V_BOARD and GND for connection to additional external hardware.

## Debugging and Test Points

A green debug LED is connected to the Curiosity Nano through a 1.2 kΩ current-limiting resistor.

A momentary debug pushbutton is provided with a 10 kΩ pull-up resistor and a 1 µF capacitor for hardware debounce.

Five test points are included for important power, ground, and ADC-related signals to support debugging and subsystem verification.
