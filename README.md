## Flashing Guide for AT89S52 Using ArduinoISP and AVRDUDE

### Objectives
- Avoid using proprietary or GUI software during the development of 8051 based systems
- Arduino is commonly avaliable than specific programmer such as the [USBasp](https://www.fischl.de/usbasp/)
- AVRDUDE officialy supports AT89S52/AT89S51

### Steps

#### Hardware Connections

![schematic][schematic1]

[schematic1]: ./images/schematic.png "Schematic of Arduino UNO as ISP and AT89S52"
```
+---------+---------+
| Arduino | AT89S52 |
+---------+---------+
| 10      | RST     |
+---------+---------+
| 11/MOSI | P1.5    |
+---------+---------+
| 12/MISO | P1.6    |
+---------+---------+
| 13/SCK  | P1.7    |
+---------+---------+
| 5V      | VCC     |
+---------+---------+
| GND     | GND     |
+---------+---------+
| 5V      | EA/VPP  |
+---------+---------+
```

#### Preparing Your Arduino to be a In Serial Programmer (ISP)

2. Install [Arduino IDE](https://www.arduino.cc/en/software)
3. Connect Arduino to your computer via USB cable
4. Open `Files > Examples > 11.ArduinoISP", flash it to the Arduino


#### Install AVRDUDE

1. Install [AVRDUDE](https://github.com/avrdudes/avrdude/releases)
2. For Windows user, choose `avrdude-v8.0-windows-x86.zip` under assets

#### Start Flashing (Linux)

A sample program is provided `blink.hex` in this repository, it will toggle `P1.0` on and off. We will flash this file in the following steps.

```
avrdude -c stk500v1 -P /dev/ttyUSB0 -b 19200 -p at89s52 -U flash:w:blink.hex:i
```
#### Start Flashing (Windows)

1. Download and copy the `blink.hex` to where your AVRDUDE is extracted
2. In file explorer, Shift + Right Click, open terminal here
3. Paste:

```
avrdude.exe -c stk500v1 -P COM1 -p at89s52 -b 19200 -U flash:w:blink.hex:i
```
Change `COM1` or `/dev/ttyUSB0` to the serial port of your Arduino. It can be checked in Arduino IDE in the select board and port section.

Replace `blink.hex` with the path of your compiled firmware.

#### Output
````
Reading 22 bytes for flash from input file blink.hex
Writing 22 bytes to flash
Writing | ################################################## | 100% 0.51 s 
Reading | ################################################## | 100% 0.18 s 
22 bytes of flash verified

Avrdude done.  Thank you.
````

### Resources

1. [AT89S52 Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/doc1919.pdf)
2. [AVRDUDE Manual](https://avrdudes.github.io/avrdude/8.0/avrdude.pdf)


### Assemblers for MCS-51

1. [ASEM-51](https://plit.de/asem-51/home.htm)
2. [Small Device C Compiler (SDCC)](https://sdcc.sourceforge.net/) - Use the sdas8051 assembler that comes with it
3. [Keil PK51](https://developer.arm.com/Tools%20and%20Software/Keil%20PK51) - This is a full blown IDE with assembler and compiler