---
title: Bill of Materials
---

# Bill of Materials

## Overview

The following Bill of Materials lists the components used in the
Fill-A-Bot Liquid Amount Sensing subsystem. The subsystem uses a 1 kg
load cell and NAU7802KGI 24-bit ADC to measure liquid weight, a
PIC18F57Q43 Curiosity Nano for processing and control, and direct
digital TEAM_IN and TEAM_OUT signals for communication with the
team controller.

## Bill of Materials

*Table 1: Liquid Amount Sensing subsystem Bill of Materials*

| **Ref.** | **Qty** | **Part Name / Description** | **Manufacturer** | **Manufacturer Part Number** | **Specification / Value** |
| --- | ---: | --- | --- | --- | --- |
| U1 | 1 | Load-cell ADC | Nuvoton Technology | NAU7802KGI | 24-bit sigma-delta ADC with PGA, 16-PDIP |
| U2 | 1 | Microcontroller development board | Microchip Technology | PIC18F57Q43 Curiosity Nano | PIC18F57Q43 Curiosity Nano |
| U3 | 1 | 5 V linear regulator | Texas Instruments | LM7805CT | Fixed 5 V, TO-220, THT |
| LC1 | 1 | Load cell | Soldered Electronics | 555026 / 100382 | 1 kg, 5-10 V excitation, 2 ±0.1 mV/V |
| J1 | 1 | Team connector | Assmann | AWH 08G-0502-T | 8-position, 2×4, 2.54 mm, shrouded THT |
| J2 | 1 | Load-cell connector | On Shore Technology | OSTVN04A150 | 4-position, 2.54 mm screw terminal, THT |
| J3 | 1 | 9-12 V power input connector | Dinkle | EK508V-02P | 2-position, 5.08 mm screw terminal, THT |
| J4 | 1 | GPIO expansion header | Amphenol | 10129378-906002BLF | 1×6, 2.54 mm male header, THT |
| FH1 | 1 | PCB fuse holder | Würth Elektronik | 952017100000000 | 5×20 mm cartridge fuse holder, THT |
| F1 | 1 | Fuse | Weidmüller | 0430600000 | 500 mA, 250 V, quick-acting, 5×20 mm |
| JP2 | 1 | Local 5 V select jumper | Würth Elektronik | 61300211121 | 1×2, 2.54 mm, THT |
| SH1 | 1 | Jumper shunt | Würth Elektronik | 60900213421 | 2.54 mm jumper |
| TP1-TP5 | 5 | Test point | Keystone Electronics | 5001 | Miniature THT test point |
| LED1 | 1 | Status / debug LED | Kingbright | WP7113LZGCK | Green, 5 mm, THT |
| SW1 | 1 | Tare / zero pushbutton | Omron | B3F-1020 | SPST-NO momentary, 6×6 mm, THT |
| R1, R2 | 2 | ADC input resistor | YAGEO | MFR-25FTE52-47R | 47 Ω, ±1%, 1/4 W |
| R3 | 1 | LED current-limiting resistor | YAGEO | MFR-25FTE52-1K2 | 1.2 kΩ, ±1%, 1/4 W |
| R4 | 1 | Button pull-up resistor | YAGEO | MFR-25FTF52-10K | 10 kΩ, ±1%, 1/4 W |
| R5, R6 | 2 | NAU7802 digital-interface pull-up resistor | YAGEO | MFR-25FRF52-4K7 | 4.7 kΩ, ±1%, 1/4 W, THT |
| C1 | 1 | LM7805 input capacitor | TDK | FA24X8R1E334KNU06 | 0.33 µF, 25 V, ceramic THT |
| C2 | 1 | LM7805 output capacitor | TDK | FA28X8R1E104KNU06 | 0.1 µF, 25 V, ceramic THT |
| C3, C4 | 2 | ADC filter / VBG capacitor | KEMET | C320C104K3R5TA | 0.1 µF, 25 V, X7R, THT |
| C5, C6 | 2 | ADC supply capacitor | TDK | FG18X7R1E105KRT06 | 1 µF, 25 V, X7R, THT |
| C7 | 1 | Button debounce capacitor | TDK | FG18X7R1E105KRT06 | 1 µF, 25 V, X7R, THT |
| C8 | 1 | Curiosity Nano bypass capacitor | KEMET | C320C104K3R5TA | 0.1 µF, 25 V, X7R, THT |

## Notes

The NAU7802KGI is mounted directly on the subsystem PCB rather than using
a separate ADC daughter board. The team interface uses J1 Pin 1 as TEAM_IN,
J1 Pin 2 as TEAM_OUT, and J1 Pin 8 as the common ground. Pins 3 through 7
of J1 are unused by this subsystem.
