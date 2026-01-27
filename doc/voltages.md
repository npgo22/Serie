# Regulators
A set of voltage regulators can be seen on the regulators sheet. They are as follows:

|Regulator|Rail |Purpose|
|---------|-----|-------|
|AP64500  |+12V |For fans|
|AP64500  |+5V  |For digital +5V peripherals|
|AP2112K  |+3.3V|For low-power 3.3V peripherals|
|TPS7A2   |+4.V |Specifically for the load cell|

For each of them, a set of 22uF capacitors are used in parallel to lower ESR/ESL and to raise the effective capcitance. The AP64500 uses frequency spread techniques to decrease noise among a few other tricks, which is important for our application. Ripple current is managed by the aforementioned 22uF capacitor sets. 

## AP64500 General
Generally, we do not use the UVLO feature as it adds complexity to the BOM and the case of a brownout doesn't really affect anything. Furthermore, a target switching frequency of 500 kHz is used as is standard to simplify math. This gives us the value for the RT/CLK pin of $200\mathrm{k\Omega}$.

We do not require power sequencing for this application, either, so we just tie EN to VIN.

### AP64500 Math
We already use $10\mathrm{k\Omega}$ resistors elsewhere in the design, so to calculate R1:

$$ R_1 = R_2 \cdot (\frac{V_{out}}{0.8\mathrm{V}} - 1) = 10,000\cdot(\frac{12\mathrm{V}}{0.8\mathrm{V}} - 1) = 140\mathrm{k\Omega}$$
$$ R_1 = R_2 \cdot (\frac{V_{out}}{0.8\mathrm{V}} - 1) = 10,000\cdot(\frac{5\mathrm{V}}{0.8\mathrm{V}} - 1) = 52.5\mathrm{k\Omega}$$

The closest E96 values for these are $140\mathrm{k\Omega}$ exact and $52.3\mathrm{k\Omega}$.

Now for the inductor at the top of our expected input voltage:
$$L = V_{out}\cdot\frac{(V_{in}-V_{out})}{V_{in}\cdot\Delta I_L \cdot f_{sw}} = \frac{12\mathrm{V}\cdot(24\mathrm{V}-12\mathrm{V})}{24\mathrm{V}\cdot2.5\mathrm{A}\cdot500,000} = 4.8\mathrm{\mu H}$$

$$L = V_{out}\cdot\frac{(V_{in}-V_{out})}{V_{in}\cdot\Delta I_L \cdot f_{sw}} = \frac{5\mathrm{V}\cdot(24\mathrm{V}-5\mathrm{V})}{24\mathrm{V}\cdot2.5\mathrm{A}\cdot500,000} = 3.167\mathrm{\mu H}$$


Now we should round up because a standard LED strip power supply can be cranked up in excess of the rated output voltage. As such, we will use inductor values of $6.8\mathrm{\mu H}$ and $3.3\mathrm{\mu H}$ far above our expected carrying current capacity of 5A, respectively.

## LDOs
For both, we just used a handfull of input and output capacitors to minimize ripple. The LDOs used have really good high-frequency PSRRs, so we don't really worry about any sort of filtering past this. 

For USB power, only the main USB power is considered. This is just to simplify power plane management, and the scenarios wherein you would only have 1 USB port available are far and few between.

A diode is applied on the 5V regulator's output to prevent backflow when external USB power is supplied.

The +4.5V regulator was chosen in accordance with the minimum USB voltage of +4.8V minus the dropout.