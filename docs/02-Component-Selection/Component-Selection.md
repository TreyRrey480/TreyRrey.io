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
…
Yes. This Component Selection page is still partly the old HX711 design, so we need to update it to match the final schematic.

The Load Cell Selection section is mostly good. The ADC selection, rationale, and pin table are what really need changing.

1. Load Cell Selection
Keep the three-option comparison and keep:

Choice: Option 1 — Soldered Electronics 555026 / 100382

But change the end of your rationale. Right now it says the manufacturer recommends the HX711 and then implies compatibility with your selected ADC. Since you're actually using the NAU7802, I'd use this finished version:

Choice: Option 1: Soldered Electronics 555026 1 kg Load Cell

Rationale: The Soldered Electronics 555026 was selected because its 1 kg maximum load provides an appropriate measurement range for the liquid container used in the Fill-A-Bot. The sensor operates from a 5 V to 10 V excitation supply and produces a 2 ±0.1 mV/V differential output from its Wheatstone bridge. This allows the load cell to operate from the subsystem's regulated 5 V supply and interface with a high-resolution bridge-sensor ADC. Although this option is more expensive than the Adafruit load cell, its documented electrical characteristics, 1 kg measurement range, and compatibility with the selected NAU7802 load-cell ADC make it well suited for the Liquid Amount Sensing subsystem.

The load-cell datasheet supports the 1 kg capacity, 5–10 V excitation and 2 ±0.1 mV/V output. 

2. ADC selection — this is the big change
Your comparison table can stay. Having the HX711, NAU7802 and ADS1232 as the three candidates is good.

But change:

Choice: Option 1: SparkFun SEN-13879 HX711

to:

Choice: Option 2: Nuvoton Technology NAU7802KGI

Then replace the HX711 rationale with:

Choice: Option 2: Nuvoton Technology NAU7802KGI

Rationale: The Nuvoton Technology NAU7802KGI was selected because it combines a 24-bit sigma-delta ADC with a programmable gain amplifier designed for precision bridge and strain-gauge measurements. Its programmable gain allows the very small differential output of the load cell to be amplified before analog-to-digital conversion. The device operates from 2.7 V to 5.5 V, making it compatible with the subsystem's regulated 5 V supply. The NAU7802KGI is also available in a 16-PDIP through-hole package, allowing the ADC to be integrated directly onto the subsystem PCB without using a separate daughter board. At approximately $2.26 per device, it is also significantly less expensive than the HX711 breakout board and ADS1232 option. These characteristics make the NAU7802KGI the best fit for the final Liquid Amount Sensing subsystem.

3. Update the NAU7802 pros/cons slightly
Your Option 2 row is already pretty good. I'd keep most of it.

One wording change:

I2C-compatible interface

can stay here because this is describing the NAU7802 IC itself, not your team-board communication.

Also keep:

Bare IC requires additional support circuitry

because your final schematic actually demonstrates that—you added the filter capacitors, resistors, pull-ups, etc.

4. The entire Pin Table needs replacing
The existing table is still entirely HX711-based.

Delete it and use your final hardware connections instead:

Component	Pin / Signal	Connection	Purpose
Soldered 555026 Load Cell	E+ / Input+	+5V_BOARD	Positive bridge excitation
Soldered 555026 Load Cell	E− / Input−	GND	Negative bridge excitation
Soldered 555026 Load Cell	A+ / Output+	R2 → NAU7802 VIN1P	Positive differential measurement
Soldered 555026 Load Cell	A− / Output−	R1 → NAU7802 VIN1N	Negative differential measurement
NAU7802KGI	VIN1P	Load cell A+ through 47 Ω	Positive ADC differential input
NAU7802KGI	VIN1N	Load cell A− through 47 Ω	Negative ADC differential input
NAU7802KGI	SDIO	PIC RB2	ADC digital data
NAU7802KGI	SCLK	PIC RB1	ADC digital clock
NAU7802KGI	DRDY	PIC RC0	Indicates new ADC conversion is ready
PIC18F57Q43	RA3	J1 Pin 1 — TEAM_IN	Direct digital input from team controller
PIC18F57Q43	RA4	J1 Pin 2 — TEAM_OUT	Direct digital output to team controller
PIC18F57Q43	RA0	SW1 TARE/ZERO	Tare/zero button input
PIC18F57Q43	RC1	R3 → LED1	Status LED output
J1	Pin 1	TEAM_IN	Team direct digital input
J1	Pin 2	TEAM_OUT	Team direct digital output
J1	Pins 3–7	NC	Unused
J1	Pin 8	GND	Common team ground
That also makes your documentation consistent with the block diagram we just rebuilt.

So don't rewrite the whole page
You only need to make three meaningful changes:

Load-cell rationale: remove the HX711-centered ending.

ADC choice: change Option 1 HX711 → Option 2 NAU7802KGI and replace its rationale.

Pin table: replace the HX711 table with the final NAU7802/PIC/team connections.

Do those and your Component Selection page will finally match the current PCB design.

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
…
Yes — this is the old version. Here is the complete updated Component Selection Markdown so you can replace the page instead of editing it piece by piece.

title: Component Selection
Component Selection
Individual Subsystem: Liquid Amount Sensing

The Liquid Amount Sensing subsystem measures the amount of liquid in the Fill-A-Bot using a load cell. The small differential signal from the load cell must be amplified and converted into digital data before it can be processed by the PIC18F57Q43 microcontroller. The following sections compare potential load cells and load-cell ADC/amplifier solutions for this subsystem.

Load Cell Selection
Table 1: Load cell component selection

Load Cell / Weight Sensor

Solution	Pros	Cons

Option 1
Soldered Electronics 555026
1 kg Load Cell
$15.96/each
Link to product	* 1 kg maximum load is appropriate for the liquid container
* Operates from 5 V to 10 V
* 2 ±0.1 mV/V output sensitivity
* Wheatstone bridge design works with a high-resolution load-cell ADC
* Detailed electrical characteristics are available from the manufacturer	* More expensive than the Adafruit option
* Requires an ADC/amplifier to measure the small output signal
* Requires calibration
* DigiKey currently lists the part as out of stock

Option 2
Adafruit Industries 4540
1 kgf Load Cell
$3.95/each
Link to product	* 1 kg measurement range is appropriate for the project
* Lowest-cost load cell of the three options
* Compact load-cell design
* Large quantity available from DigiKey	* Requires an external ADC/amplifier
* Requires calibration before accurate measurements can be made
* Available documentation provides less electrical information than the Soldered load cell

Option 3
Seeed Technology 314990000
0-500 g Load Cell
$17.00/each
Link to product	* Designed for electronic weighing applications
* Recommended 5 V excitation matches the subsystem supply
* 0.5 ±0.1 mV/V output sensitivity
* ±0.05% full-scale nonlinearity specification	* Maximum capacity is only 500 g
* Container plus liquid could exceed the 500 g limit
* Most expensive load-cell option
* Requires an external ADC/amplifier
Choice: Option 1: Soldered Electronics 555026 1 kg Load Cell

Rationale: The Soldered Electronics 555026 was selected because its 1 kg maximum load provides an appropriate measurement range for the liquid container used in the Fill-A-Bot. The sensor operates from a 5 V to 10 V excitation supply and produces a 2 ±0.1 mV/V differential output from its Wheatstone bridge. This allows the load cell to operate from the subsystem's regulated 5 V supply and interface with a high-resolution bridge-sensor ADC. Although this option is more expensive than the Adafruit load cell, its documented electrical characteristics, 1 kg measurement range, and compatibility with the selected NAU7802 load-cell ADC make it well suited for the Liquid Amount Sensing subsystem.

Load Cell ADC / Amplifier Selection
Table 2: Load cell ADC/amplifier component selection

Load Cell ADC / Amplifier

Solution	Pros	Cons

Option 1
SparkFun Electronics SEN-13879
HX711 Load Cell Amplifier
$11.50/each
Link to product	* 24-bit ADC designed specifically for weigh scales and bridge sensors
* Built-in low-noise programmable gain amplifier
* Selectable gain of 32, 64, or 128
* Operates from 2.6 V to 5.5 V
* Complete breakout board simplifies prototyping
* Simple clock and data interface to the microcontroller	* More expensive than a bare ADC IC
* Maximum standard sample rate is 80 SPS
* Breakout-board implementation is not appropriate for direct integration into the final subsystem PCB
* Requires software calibration for accurate weight measurements

Option 2
Nuvoton Technology NAU7802KGI
24-bit Load Cell ADC
$2.26/each
Link to product	* 24-bit sigma-delta ADC designed for bridge and strain-gauge sensors
* Programmable gain from 1 to 128
* Digital SDIO/SCLK interface to the microcontroller
* Operates from 2.7 V to 5.5 V
* Through-hole 16-PDIP package is convenient for PCB integration
* Significantly less expensive than the HX711 module	* Bare IC requires additional support circuitry
* More software configuration is required
* Requires configuration before measurements can be taken
* More complex to integrate than a complete breakout board

Option 3
Texas Instruments ADS1232IPWR
24-bit Bridge Sensor ADC
$8.50/each
Link to product	* 24-bit ADC specifically designed for bridge sensors and weigh scales
* Low-noise programmable gain amplifier
* Selectable gains of 1, 2, 64, and 128
* Two differential input channels
* Operates from 2.7 V to 5.3 V
* 10 SPS mode provides strong 50 Hz and 60 Hz noise rejection	* Surface-mount 24-TSSOP package is more difficult to prototype
* Requires additional external support components
* More complex PCB layout than the other options
* More expensive than the NAU7802 bare IC
Choice: Option 2: Nuvoton Technology NAU7802KGI

Rationale: The Nuvoton Technology NAU7802KGI was selected because it combines a 24-bit sigma-delta ADC with a programmable gain amplifier designed for precision bridge and strain-gauge measurements. Its programmable gain allows the very small differential output of the load cell to be amplified before analog-to-digital conversion. The device operates from 2.7 V to 5.5 V, making it compatible with the subsystem's regulated 5 V supply. The NAU7802KGI is also available in a 16-PDIP through-hole package, allowing the ADC to be integrated directly onto the subsystem PCB without using a separate daughter board. At approximately $2.26 per device, it is also significantly less expensive than the HX711 breakout board and ADS1232 option. These characteristics make the NAU7802KGI the best fit for the final Liquid Amount Sensing subsystem.

Pin Table
Table 3: Liquid Amount Sensing subsystem pin connections

Component	Pin / Signal	Connection	Purpose
Soldered 555026 Load Cell	E+ / Input+	+5V_BOARD	Positive load-cell bridge excitation
Soldered 555026 Load Cell	E- / Input-	GND	Negative load-cell bridge excitation
Soldered 555026 Load Cell	A+ / Output+	R2 → NAU7802 VIN1P	Positive differential load-cell signal
Soldered 555026 Load Cell	A- / Output-	R1 → NAU7802 VIN1N	Negative differential load-cell signal
NAU7802KGI	VIN1P	Load-cell A+ through 47 Ω R2	Positive differential ADC input
NAU7802KGI	VIN1N	Load-cell A- through 47 Ω R1	Negative differential ADC input
NAU7802KGI	SDIO	PIC18F57Q43 RB2	Bidirectional digital ADC data
NAU7802KGI	SCLK	PIC18F57Q43 RB1	Digital clock from PIC to ADC
NAU7802KGI	DRDY	PIC18F57Q43 RC0	Indicates that a new ADC conversion is ready
PIC18F57Q43	RA3	J1 Pin 1 - TEAM_IN	Direct HIGH/LOW input from the team controller
PIC18F57Q43	RA4	J1 Pin 2 - TEAM_OUT	Direct HIGH/LOW output to the team controller
PIC18F57Q43	RA0	SW1 TARE/ZERO	Tare/zero pushbutton input
PIC18F57Q43	RC1	R3 → LED1	Status LED output
Team Connector J1	Pin 1	TEAM_IN	Direct digital input
Team Connector J1	Pin 2	TEAM_OUT	Direct digital output
Team Connector J1	Pins 3-7	NC	Unused team-connector pins
Team Connector J1	Pin 8	GND	Common ground between team subsystems
One important improvement I made: I removed the wording that made the team communication sound like I²C. The NAU7802 still has its own SDIO/SCLK digital interface to your PIC, while J1 TEAM_IN/TEAM_OUT remains direct HIGH/LOW pin-to-pin communication.

Paste this into 02-Component-Selection in place of the old page.

code form
Yep — here is the full updated Markdown in a code block so you can copy/paste it directly into your GitHub .md file.

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
| ![](loadcell_soldered_555026.png)<br>**Option 1**<br>Soldered Electronics 555026<br>1 kg Load Cell<br>$15.96/each<br>[Link to product](https://www.digikey.com/en/products/detail/soldered-electronics/555026/29271488) | \* 1 kg maximum load is appropriate for the liquid container<br>\* Operates from 5 V to 10 V<br>\* 2 ±0.1 mV/V output sensitivity<br>\* Wheatstone bridge design works with a high-resolution load-cell ADC<br>\* Detailed electrical characteristics are available from the manufacturer | \* More expensive than the Adafruit option<br>\* Requires an ADC/amplifier to measure the small output signal<br>\* Requires calibration<br>\* DigiKey currently lists the part as out of stock |
| ![](loadcell_adafruit_4540.png)<br>**Option 2**<br>Adafruit Industries 4540<br>1 kgf Load Cell<br>$3.95/each<br>[Link to product](https://www.digikey.com/en/products/detail/adafruit-industries-llc/4540/12323569) | \* 1 kg measurement range is appropriate for the project<br>\* Lowest-cost load cell of the three options<br>\* Compact load-cell design<br>\* Large quantity available from DigiKey | \* Requires an external ADC/amplifier<br>\* Requires calibration before accurate measurements can be made<br>\* Available documentation provides less electrical information than the Soldered load cell |
| ![](loadcell_seeed_314990000.png)<br>**Option 3**<br>Seeed Technology 314990000<br>0-500 g Load Cell<br>$17.00/each<br>[Link to product](https://www.digikey.com/en/products/detail/seeed-technology-co-ltd/314990000/5488115) | \* Designed for electronic weighing applications<br>\* Recommended 5 V excitation matches the subsystem supply<br>\* 0.5 ±0.1 mV/V output sensitivity<br>\* ±0.05% full-scale nonlinearity specification | \* Maximum capacity is only 500 g<br>\* Container plus liquid could exceed the 500 g limit<br>\* Most expensive load-cell option<br>\* Requires an external ADC/amplifier |

**Choice:** Option 1: Soldered Electronics 555026 1 kg Load Cell

**Rationale:** The Soldered Electronics 555026 was selected because its
1 kg maximum load provides an appropriate measurement range for the liquid
container used in the Fill-A-Bot. The sensor operates from a 5 V to 10 V
excitation supply and produces a 2 ±0.1 mV/V differential output from its
Wheatstone bridge. This allows the load cell to operate from the subsystem's
regulated 5 V supply and interface with a high-resolution bridge-sensor ADC.
Although this option is more expensive than the Adafruit load cell, its
documented electrical characteristics, 1 kg measurement range, and
compatibility with the selected NAU7802 load-cell ADC make it well suited
for the Liquid Amount Sensing subsystem.


## Load Cell ADC / Amplifier Selection

*Table 2: Load cell ADC/amplifier component selection*

**Load Cell ADC / Amplifier**

| **Solution** | **Pros** | **Cons** |
| --- | --- | --- |
| ![](adc_hx711_13879.png)<br>**Option 1**<br>SparkFun Electronics SEN-13879<br>HX711 Load Cell Amplifier<br>$11.50/each<br>[Link to product](https://www.digikey.com/en/products/detail/sparkfun-electronics/13879/6202732) | \* 24-bit ADC designed specifically for weigh scales and bridge sensors<br>\* Built-in low-noise programmable gain amplifier<br>\* Selectable gain of 32, 64, or 128<br>\* Operates from 2.6 V to 5.5 V<br>\* Complete breakout board simplifies prototyping<br>\* Simple clock and data interface to the microcontroller | \* More expensive than a bare ADC IC<br>\* Maximum standard sample rate is 80 SPS<br>\* Breakout-board implementation is not appropriate for direct integration into the final subsystem PCB<br>\* Requires software calibration for accurate weight measurements |
| ![](adc_nau7802.png)<br>**Option 2**<br>Nuvoton Technology NAU7802KGI<br>24-bit Load Cell ADC<br>$2.26/each<br>[Link to product](https://www.digikey.com/en/products/detail/nuvoton-technology-corporation/NAU7802KGI/2769783) | \* 24-bit sigma-delta ADC designed for bridge and strain-gauge sensors<br>\* Programmable gain from 1 to 128<br>\* Digital SDIO/SCLK interface to the microcontroller<br>\* Operates from 2.7 V to 5.5 V<br>\* Through-hole 16-PDIP package is convenient for PCB integration<br>\* Significantly less expensive than the HX711 module | \* Bare IC requires additional support circuitry<br>\* More software configuration is required<br>\* Requires configuration before measurements can be taken<br>\* More complex to integrate than a complete breakout board |
| ![](adc_ads1232.png)<br>**Option 3**<br>Texas Instruments ADS1232IPWR<br>24-bit Bridge Sensor ADC<br>$8.50/each<br>[Link to product](https://www.digikey.com/en/products/detail/texas-instruments/ADS1232IPWR/1689138) | \* 24-bit ADC specifically designed for bridge sensors and weigh scales<br>\* Low-noise programmable gain amplifier<br>\* Selectable gains of 1, 2, 64, and 128<br>\* Two differential input channels<br>\* Operates from 2.7 V to 5.3 V<br>\* 10 SPS mode provides strong 50 Hz and 60 Hz noise rejection | \* Surface-mount 24-TSSOP package is more difficult to prototype<br>\* Requires additional external support components<br>\* More complex PCB layout than the other options<br>\* More expensive than the NAU7802 bare IC |

**Choice:** Option 2: Nuvoton Technology NAU7802KGI

**Rationale:** The Nuvoton Technology NAU7802KGI was selected because it
combines a 24-bit sigma-delta ADC with a programmable gain amplifier designed
for precision bridge and strain-gauge measurements. Its programmable gain
allows the very small differential output of the load cell to be amplified
before analog-to-digital conversion. The device operates from 2.7 V to 5.5 V,
making it compatible with the subsystem's regulated 5 V supply. The
NAU7802KGI is also available in a 16-PDIP through-hole package, allowing the
ADC to be integrated directly onto the subsystem PCB without using a separate
daughter board. At approximately $2.26 per device, it is also significantly
less expensive than the HX711 breakout board and ADS1232 option. These
characteristics make the NAU7802KGI the best fit for the final Liquid Amount
Sensing subsystem.


## Pin Table

*Table 3: Liquid Amount Sensing subsystem pin connections*

| **Component** | **Pin / Signal** | **Connection** | **Purpose** |
| --- | --- | --- | --- |
| Soldered 555026 Load Cell | E+ / Input+ | +5V_BOARD | Positive load-cell bridge excitation |
| Soldered 555026 Load Cell | E- / Input- | GND | Negative load-cell bridge excitation |
| Soldered 555026 Load Cell | A+ / Output+ | R2 → NAU7802 VIN1P | Positive differential load-cell signal |
| Soldered 555026 Load Cell | A- / Output- | R1 → NAU7802 VIN1N | Negative differential load-cell signal |
| NAU7802KGI | VIN1P | Load-cell A+ through 47 Ω R2 | Positive differential ADC input |
| NAU7802KGI | VIN1N | Load-cell A- through 47 Ω R1 | Negative differential ADC input |
| NAU7802KGI | SDIO | PIC18F57Q43 RB2 | Bidirectional digital ADC data |
| NAU7802KGI | SCLK | PIC18F57Q43 RB1 | Digital clock from PIC to ADC |
| NAU7802KGI | DRDY | PIC18F57Q43 RC0 | Indicates that a new ADC conversion is ready |
| PIC18F57Q43 | RA3 | J1 Pin 1 - TEAM_IN | Direct HIGH/LOW input from the team controller |
| PIC18F57Q43 | RA4 | J1 Pin 2 - TEAM_OUT | Direct HIGH/LOW output to the team controller |
| PIC18F57Q43 | RA0 | SW1 TARE/ZERO | Tare/zero pushbutton input |
| PIC18F57Q43 | RC1 | R3 → LED1 | Status LED output |
| Team Connector J1 | Pin 1 | TEAM_IN | Direct digital input |
| Team Connector J1 | Pin 2 | TEAM_OUT | Direct digital output |
| Team Connector J1 | Pins 3-7 | NC | Unused team-connector pins |
| Team Connector J1 | Pin 8 | GND | Common ground between team subsystems |
You can Ctrl+A the old Component Selection Markdown, delete it, paste this entire block, then commit the changes.
a



⋮⋮⋮⋮⋮⋮⋮⋮⋮⋮⋮⋮
