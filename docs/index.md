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
produces a very small differential voltage, a load-cell ADC/amplifier is
used to amplify and digitize the signal before it is processed by the
PIC18F57Q43 microcontroller.

### Project Summary

The Fill-A-Bot is a team embedded-systems project consisting of multiple
subsystems that work together to control and monitor the movement and
dispensing of liquid.

My portion of the project is the Liquid Amount Sensing subsystem. Its
purpose is to measure the amount of liquid present so that the system can
monitor changes in liquid quantity and provide measurement data to the
main controller.

The subsystem is based around a load cell, load-cell ADC/amplifier, and
PIC18F57Q43 microcontroller.

### My Contribution

My individual contribution is the design and implementation of the
Liquid Amount Sensing subsystem. This includes selecting the sensing
components, designing the electrical connections, interfacing the sensor
electronics with the PIC18F57Q43, and documenting the subsystem.

The major components selected for the subsystem are a Soldered Electronics
555026 1 kg load cell and a SparkFun SEN-13879 HX711 load-cell
ADC/amplifier.

The following sections document the development of my subsystem:

* [Block Diagram](01-Block-Diagram/Block-Diagram.md)
* [Component Selection](02-Component-Selection/Component-Selection.md)
* [Bill of Materials](03-BOM/BOM.md)
* [Schematic](04-Schematic/Schematic.md)
* [Power Budget](05-Power-Budget/Power-Budget.md)
