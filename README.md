# Serie
Serie is a basic mainboard built to handle:
1. Insanely high temperatures
2. Insanely high speeds
3. Several axis of movement

The board itself is based around an STM32H723, the fastest microcontroller supported by Klipper at the moment.

## I/O
Currently, the following I/O is planned:

### Temperature sensing
Four MAX31865 modules will be integrated for temperature sensing to be used as follows:
1. Hotend
2. Bed
3. Chamber
4. Spare/standby

Several other standard thermistor inputs will be broken out as needed.

### Motors
There will be 6-8x motors driven by TMC2241s. Each TMC2241 will likely have a *polymer* electrolytic cap on each, and will be mounted on the right side of the board because putting them upside down looks silly. Support to klipper will need to be added to support this.

### Load Cell
There should be a separate input for a load cell. That's about it.

### Isolated Inputs
There should be at least 15 digitally isolated inputs.

### Low Power Outputs
There should be at least 15 outputs driven by small MOSFETs for outputs to other devices.

### Buses
As many buses should be broken out as possible.

### 12V Outputs
There should be a decent select of moderately powerful 12V outputs to drive peripherals such as fans.

### Additional Current Sensing
There should be an additional set of current sensing transformers for safety reasons.

### USB
There will be at least 1 USB-C input.

## Power
As of right now, it is planned to require an external 48V power supply for the motors and a 12V power supply for the mainboard. This maintains galvanic isolation while providing decent protection against  A small switching regulator will generate 5V (AP62300TWU-7 + ETQP4MR68KVK) which will then be fed into a 2112K-3.3. For some reason everyone still uses 1117's despite the fact that they can't be used with low esr caps. Like seriously, does nobody notice the very clear resonances at 1-100 kHz from their PDN?

### Heaters
Bed and chamber will be mains-powered, hotend heater cartridge will be 48V (sharing the motor's supply), and all the fans will maintain 12V.

#### Switching
Mains powered items will be driven by an IGBT, which necessitates the selection of a decent gate driver.

### Motors
Motors will be powered by a separate 48V power supply as they are extremely noisy.

## Board construction
Probably 4 layers. Don't really need more at this time.

## Misc.
* Consider additional I/O such as ethernet, SD cards, and another USB port for a flash drive
* Consider a dedicated output for an LCD
* Consider adding circuitry for eddy current detection (works by simply exciting a coil then measuring the change in impedance as eddy currents are induced into the coil).
* Consider adding an opamp set for piezo trigger detection.
* Consider a standardized header for breaking out to other boards.
* Total BoM cost for 2x is expected to be in the neighborhood of $150 once it's all assembled.