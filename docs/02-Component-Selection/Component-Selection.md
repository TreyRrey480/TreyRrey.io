---
title: Component Selection
---

# Component Selection
**Individual Subsystem: Liquid Amount Sensing**

The Liquid Amount Sensing subsystem measures the amount of liquid in the
Fill-A-Bot using a load cell. The small differential signal from the load cell
must be amplified and converted into digital data before it can be processed
by the PIC18F57Q43 microcontroller. The following sections compare potential
load cells and load-cell ADC/amplifier solutions for this subsystem.


## Load Cell Selection

*Table 1: Load cell component selection*

**Load Cell / Weight Sensor**

| **Solution** | **Pros** | **Cons** |
| --- | --- | --- |
| ![](loadcell_soldered_555026.png)<br>**Option 1**<br>Soldered Electronics 555026<br>1 kg Load Cell<br>$15.96/each<br>[Link to product](https://www.digikey.com/en/products/detail/soldered-electronics/555026/29271488) | \* 1 kg maximum load is appropriate for the liquid container<br>\* Operates from 5 V to 10 V<br>\* 2 ±0.1 mV/V output sensitivity<br>\* Wheatstone bridge design works with a load-cell ADC<br>\* Manufacturer specifically recommends an HX711 interface | \* More expensive than the Adafruit option<br>\* Requires an ADC/amplifier to measure the small output signal<br>\* Requires calibration<br>\* DigiKey currently lists the part as out of stock |
| ![](loadcell_adafruit_4540.png)<br>**Option 2**<br>Adafruit Industries 4540<br>1 kgf Load Cell<br>$3.95/each<br>[Link to product](https://www.digikey.com/en/products/detail/adafruit-industries-llc/4540/12323569) | \* 1 kg measurement range is appropriate for the project<br>\* Lowest-cost load cell of the three options<br>\* Compact load-cell design<br>\* Large quantity available from DigiKey | \* Requires an external ADC/amplifier<br>\* Requires calibration before accurate measurements can be made<br>\* Available documentation provides less electrical information than the Soldered load cell |
| ![](loadcell_seeed_314990000.png)<br>**Option 3**<br>Seeed Technology 314990000<br>0-500 g Load Cell<br>$17.00/each<br>[Link to product](https://www.digikey.com/en/products/detail/seeed-technology-co-ltd/314990000/5488115) | \* Designed for electronic weighing applications<br>\* Recommended 5 V excitation matches the subsystem supply<br>\* 0.5 ±0.1 mV/V output sensitivity<br>\* ±0.05% full-scale nonlinearity specification | \* Maximum capacity is only 500 g<br>\* Container plus liquid could exceed the 500 g limit<br>\* Most expensive load-cell option<br>\* Requires an external ADC/amplifier |

**Choice:** Option 1: Soldered Electronics 555026 1 kg Load Cell

**Rationale:** The Soldered Electronics 555026 was selected because its
1 kg maximum load provides an appropriate measurement range for the liquid
container used in the Fill-A-Bot. The sensor operates from a 5 V to 10 V
excitation supply and produces a 2 ±0.1 mV/V output from its Wheatstone
bridge. This allows it to operate from the subsystem's 5 V supply and
interface with a high-resolution load-cell ADC. The manufacturer's
documentation also specifically recommends using an HX711 to amplify and
digitize the small load-cell output. Although this option is more expensive
than the Adafruit load cell, its documented electrical characteristics and
compatibility with the selected ADC provide greater confidence in the final
design.


## Load Cell ADC / Amplifier Selection

*Table 2: Load cell ADC/amplifier component selection*

**Load Cell ADC / Amplifier**

| **Solution** | **Pros** | **Cons** |
| --- | --- | --- |
| ![](adc_hx711_13879.png)<br>**Option 1**<br>SparkFun Electronics SEN-13879<br>HX711 Load Cell Amplifier<br>$11.50/each<br>[Link to product](https://www.digikey.com/en/products/detail/sparkfun-electronics/13879/6202732) | \* 24-bit ADC designed specifically for weigh scales and bridge sensors<br>\* Built-in low-noise programmable gain amplifier<br>\* Selectable gain of 32, 64, or 128<br>\* Operates from 2.6 V to 5.5 V<br>\* Complete breakout board simplifies prototyping<br>\* Simple clock and data interface to the microcontroller | \* More expensive than a bare ADC IC<br>\* Maximum standard sample rate is 80 SPS<br>\* Does not use the standard I2C protocol<br>\* Requires software calibration for accurate weight measurements |
| ![](adc_nau7802.png)<br>**Option 2**<br>Nuvoton Technology NAU7802KGI<br>24-bit Load Cell ADC<br>$2.26/each<br>[Link to product](https://www.digikey.com/en/products/detail/nuvoton-technology-corporation/NAU7802KGI/2769783) | \* 24-bit sigma-delta ADC designed for bridge and strain-gauge sensors<br>\* Programmable gain from 1 to 128<br>\* I2C-compatible interface<br>\* Operates from 2.7 V to 5.5 V<br>\* Through-hole 16-PDIP package is convenient for prototyping<br>\* Significantly less expensive than the HX711 module | \* Bare IC requires additional support circuitry<br>\* More software configuration is required<br>\* Requires register configuration over I2C<br>\* More complex to integrate than a complete breakout board |
| ![](adc_ads1232.png)<br>**Option 3**<br>Texas Instruments ADS1232IPWR<br>24-bit Bridge Sensor ADC<br>$8.50/each<br>[Link to product](https://www.digikey.com/en/products/detail/texas-instruments/ADS1232IPWR/1689138) | \* 24-bit ADC specifically designed for bridge sensors and weigh scales<br>\* Low-noise programmable gain amplifier<br>\* Selectable gains of 1, 2, 64, and 128<br>\* Two differential input channels<br>\* Operates from 2.7 V to 5.3 V<br>\* 10 SPS mode provides strong 50 Hz and 60 Hz noise rejection | \* Surface-mount 24-TSSOP package is more difficult to prototype<br>\* Requires additional external support components<br>\* More complex PCB layout than the HX711 breakout board<br>\* More expensive than the NAU7802 bare IC |

**Choice:** Option 1: SparkFun Electronics SEN-13879 HX711 Load Cell Amplifier

**Rationale:** The SparkFun SEN-13879 HX711 was selected because the HX711
is specifically designed to interface directly with Wheatstone-bridge load
cells. It combines a 24-bit ADC with a low-noise programmable gain amplifier,
allowing the very small differential output from the selected load cell to be
measured without a separate external amplifier. The device operates from
2.6 V to 5.5 V, making it compatible with the subsystem's 5 V supply. The
SparkFun board also contains the supporting circuitry needed for the HX711,
which simplifies prototyping and reduces PCB design risk. Although the
NAU7802 is less expensive and provides an I2C-compatible interface, the
complete HX711 breakout board provides the simplest implementation for the
Liquid Amount Sensing subsystem.

## Pin Table

*Table 3: Liquid Amount Sensing subsystem pin connections*

| **Component** | **Pin / Signal** | **Connection** | **Purpose** |
| --- | --- | --- | --- |
| Soldered 555026 Load Cell | Red - Input+ | HX711 E+ | Positive load-cell excitation |
| Soldered 555026 Load Cell | Black - Input- | HX711 E- | Negative load-cell excitation |
| Soldered 555026 Load Cell | Green - Output+ | HX711 A+ | Positive differential load-cell signal |
| Soldered 555026 Load Cell | White - Output- | HX711 A- | Negative differential load-cell signal |
| SparkFun SEN-13879 HX711 | VCC | 5 V | Power for HX711 module |
| SparkFun SEN-13879 HX711 | GND | GND | Common system ground |
| SparkFun SEN-13879 HX711 | DOUT | PIC18F57Q43 GPIO | Serial load-cell measurement data |
| SparkFun SEN-13879 HX711 | PD_SCK | PIC18F57Q43 GPIO | HX711 serial clock |
