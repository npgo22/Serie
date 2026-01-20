# Serie
Serie is a basic mainboard built to handle:
1. Insanely high temperatures
2. Insanely high speeds
3. Several axis of movement

The board itself is based around an STM32H723, the fastest microcontroller supported by Klipper at the moment.

## I/O
Currently, the following I/O is planned:

### Temperature sensing
Four MAX31856 (for type-k thermocouples) modules will be integrated for temperature sensing to be used as follows:
1. Hotend
2. Bed
3. Chamber
4. Spare/standby

Several other standard thermistor inputs will be broken out as needed.

### Motors
There will be 6x motors driven by TMC2241s. Each TMC2241 Support to klipper will need to be added to support this.

### Isolated Inputs
There are 16 digitally isolated inputs.

### Low Power Outputs
There are 6 outputs driven by small MOSFETs for outputs to other devices.

### Buses
As many buses should be broken out as possible.

### 12V Outputs
There are four 12V outputs to drive peripherals such as fans.

### USB
There will be at least 1 USB-C input.

### Ethernet
As I have ethernet stuff on hand, this board will have ethernet.

### Piezo Inputs
There will be a transimpedance amplifier followed by an instrumentation amplifier and an external comparator for piezo measurement. This is because the beacon probe cannot handle higher temperatures.

### Endstops
The enstops will utilize optoisolated inputs, and will be 3 pins to accomodate hall effect sensors.

## Power
As of right now, it is planned to require an external 48V power supply for the motors and a 12V power supply for the mainboard. This maintains galvanic isolation while providing decent protection against  A small switching regulator will generate 5V (AP62300TWU-7 + ETQP4M3R3KVK) which will then be fed into a 2112K-3.3.

### Heaters
Bed and chamber will be mains-powered, and motors will see 48V to 60V. and all the fans will maintain 12V, and the hotend heater cartridge will be able to handle 24V but will require a separate power supply just for it.

#### Switching
Mains powered items will be driven by an SSR, which necessitates the selection of a decent gate driver.

### Motors
Motors will be powered by a separate 48V power supply as they are extremely noisy.

## Board construction
Probably 4 layers. Don't really need more at this time.

## Misc.
* Consider a standardized header for breaking out to other boards.
* Total BoM cost for 2x is expected to be in the neighborhood of $150 once it's all assembled.