---
title: Welcome
tags:
  - EGR304
  - Liquid Amount Sensing
---

<center>
<font size="6">Troy Reynolds Datasheet</font><br>
as part of<br>
<font size="8">Fill-A-Bot</font><br>
for<br>
<font size="5">Team 201</font><br>

**Individual Subsystem: Liquid Amount Sensing**
</center>

## Introduction

This datasheet documents the design and development of my individual
Liquid Amount Sensing subsystem for the Fill-A-Bot project. The subsystem
is responsible for measuring the amount of liquid in the system and
providing this information to the rest of the embedded system.

The subsystem uses a load cell to measure weight. Because a load cell
produces a very small differential voltage, a load-cell ADC with a
programmable gain amplifier is used to amplify and digitize the signal
before it is processed by the PIC18F57Q43 microcontroller.

### Project Summary

The Fill-A-Bot is a team embedded-systems project consisting of multiple
subsystems that work together to control and monitor the movement and
dispensing of liquid.

My portion of the project is the Liquid Amount Sensing subsystem. Its
purpose is to measure the amount of liquid present so that the system can
monitor changes in liquid quantity and provide measurement data to the
main controller.

The subsystem is based around a 1 kg load cell, NAU7802KGI 24-bit
load-cell ADC, and PIC18F57Q43 microcontroller.

### My Contribution

My individual contribution is the design and implementation of the
Liquid Amount Sensing subsystem. This includes selecting the sensing
components, designing the electrical connections, interfacing the sensor
electronics with the PIC18F57Q43, developing the subsystem power and
communication interfaces, and documenting the subsystem.

The major components selected for the subsystem are an Adafruit Industries
4540 1 kg load cell and a Nuvoton Technology NAU7802KGI
24-bit load-cell ADC with a programmable gain amplifier.

The NAU7802 communicates locally with the PIC18F57Q43 using SDIO, SCLK,
and DRDY. Communication between the Liquid Amount Sensing subsystem and
the Fill-A-Bot main controller uses four direct digital signals. C1 and
C0 are command inputs from the main controller, while S1 and S0 are
status outputs from the Liquid Amount Sensing subsystem.

The following sections document the development of my subsystem:

* [Block Diagram](01-Block-Diagram/Block-Diagram.md)
* [Component Selection](02-Component-Selection/Component-Selection.md)
* [Bill of Materials](03-BOM/BOM.md)
* [Schematic](04-Schematic/schematic.md)
* [Power Budget](05-Power-Budget/Power-Budget.md)
