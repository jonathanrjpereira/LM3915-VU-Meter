# LM3915 VU Meter
An audio volume level indicator using the LM3915.

**Order PCB:**

## Electronic Components
| Qty | Component | Buy |
| ------------- | ------------- | ------------- |
| 1 | 555 |[AliExpress](http://s.click.aliexpress.com/e/sCv1ACC) |
| 2 | 3KΩ Resistor |[AliExpress](http://s.click.aliexpress.com/e/bh4eqrQs) |
| 4 | 10KΩ Resistor |[AliExpress](http://s.click.aliexpress.com/e/bh4eqrQs) |
| 1 | 1MΩ Potentiometer |[AliExpress](http://s.click.aliexpress.com/e/bR23nRuG) |
| 1 | IN4004 Diode |[AliExpress](http://s.click.aliexpress.com/e/HW1fm16) |
| 2 | Tactile Momentary Push Buttons |[AliExpress](http://s.click.aliexpress.com/e/c77Ajrpq) |
| 2 | 5mm LED |[AliExpress](http://s.click.aliexpress.com/e/wuFpLXS) |
| 2 | 100uF Capacitor |[AliExpress](http://s.click.aliexpress.com/e/c9FHzl5W) |
| 2 | 0.1uF (100nF) Capacitor |[AliExpress](http://s.click.aliexpress.com/e/byQG0DZW) |
| 1 | 2 Pin Screw Terminal |[AliExpress](http://s.click.aliexpress.com/e/bj5UNUs0) |
| 1 | 3 Pin Screw Terminal |[AliExpress](http://s.click.aliexpress.com/e/bj5UNUs0) |
| 1 | 12VDC Relay |[AliExpress](http://s.click.aliexpress.com/e/xyrHlu8) |
| 1 | 12VDC Adapter |[AliExpress](http://s.click.aliexpress.com/e/V0x0bms) |
| 1 | SPDT Slide Switch |[AliExpress](http://s.click.aliexpress.com/e/cDjWUvjK) |
| 1 | PCB |[AliExpress](http://s.click.aliexpress.com/e/dhgwzKY) |


| Tools | Buy |
|--|--|
|Soldering Iron|[AliExpress](http://s.click.aliexpress.com/e/E83bSJI) |
|Soldering Wire|[AliExpress](http://s.click.aliexpress.com/e/PdhB0nm) |
|Mini PCB Hand Drill + Bits|[AliExpress](http://s.click.aliexpress.com/e/b93tomjI) |

## LM3915

The LM3915 is a monolithic integrated circuit that senses analog voltage levels and drives ten LEDs,
providing a logarithmic 3 dB/step analog display. One pin changes the display from a bar graph to
a moving dot display.

The whole display system can operate from a single supply as low as 3V or as high as 25V.

**Pinout**

The DIP package of the LM3915 has 18 pins. Most pins are used as output pins that drive the LEDs while the rest of the pins used as power supply, reference configurations and IC control.

![Pinout](https://github.com/jonathanrjpereira/LM3915-VU-Meter/blob/master/img/LM3915.png)
![Pin Description](https://github.com/jonathanrjpereira/LM3915-VU-Meter/blob/master/img/pindescription.png)

**LED Configuration**

LED current drive is regulated and programmable, eliminating the need for current limiting resistors. Hence the anodes of the LEDs are directly connected to VCC and the cathodes are connected to the LM3915. The LEDs turn ON when the driving pins of the LM3915 are set to LOW.

**Analog Voltage Reference**

The IC contains an adjustable voltage reference and an accurate ten-step voltage divider. Pins 6 and 4 are used to set the sensitivity range of the voltage divider. RHI sets the maximum voltage of the voltage divider and RLO sets the minimum voltage of the voltage divider. These pins can be connected to any voltage above 0V and 1.5V below VCC.

**Mode Select**

The LM3915 has two display modes: Bar Graph mode & Moving Dot mode.
In the Bar Graph mode, all the LEDs turn ON below a certain level. Hence if the input signal level is maximum, all the LEDs should turn ON. Whereas in Moving Dot mode only a single LED is turned ON at a time.
The mode is selected by configuring Pin 9. When Pin 9 is connected to VCC, it operates in the Bar Graph mode whereas if Pin 9 is left floating, the LM3915 operates in the Moving Dot mode.

**LED Current Programming and Setting the Internal Voltage Reference**

The reference is designed to be adjustable and develops a nominal 1.25V between the REF OUT (pin 7) and REF ADJ (pin 8) terminals.

![VREF](https://github.com/jonathanrjpereira/LM3915-VU-Meter/blob/master/img/eqn1.svg)

Since we are using only one resistor (R1), VREF = 1.25V, which is more than 1.5V below VCC.

The LED current is calculated using the following formula:

![ILED](https://github.com/jonathanrjpereira/LM3915-VU-Meter/blob/master/img/eqn2.svg)

![R](https://github.com/jonathanrjpereira/LM3915-VU-Meter/blob/master/img/eqn3.svg)

Hence if an LED requires 3mA, we will need to set the value of R to 4.7KΩ.

**Voltage Divider Working**

The voltage divider consists of ten comparators. If the non-inverting terminal(+) voltage is higher than the inverting terminal(-) voltage, the comparator comparator output is driven HIGH. The inverting terminal are all connected to the Input Signal (Pin 5). The non-inverting(+) terminals are connected through a series of resistors which create larger and larger voltage dividers. The non-inverting(+) voltage on the first comparator will be the divider input voltage (RHI − RLO), while the non-inverting(+) voltage on the last comparator is 1/10th of that voltage. Hence in order to turn ON an LED, the analog Input Signal voltage must be greater than the divided input on a comparator. So a smaller signal voltage is required to turn on the first LED in comparison to any of the following.

![Comparator](https://github.com/jonathanrjpereira/LM3915-VU-Meter/blob/master/img/comparator.png)

## LM386
The LM386 is a power amplifier designed for use in low voltage consumer applications. The gain is internally set to 20 to keep external part count low, but the addition of an external resistor and capacitor between pins 1 and 8 will increase the gain to any value from 20 to 200.

The inputs are ground referenced while the output automatically biases to one-half the supply voltage.

![Pinout](https://github.com/jonathanrjpereira/555-Electronic-Car-Horn/blob/master/img/386pinout.png)
![Pin Description](https://github.com/jonathanrjpereira/555-Electronic-Car-Horn/blob/master/img/386pindescription.png)

**Circuit:**

Electret Microphone
LM386
LM3915

The microphone is an electret type and requires a resistor to bias the capacitor connected to it. Some electret microphones also have an amplifier built-in, which also needs power. The larger the resistor from VCC the larger the voltage drop caused by the supply current, though for an unamplified electret the current is low and the resistor may be bigger.
A too small resistor will cause the signal to be attenuated. VCC is ground for AC signals and a small resistor will cause too much current to go that way. In this case the 10KΩ resistor R2 acts as the bias resistor.

The capacitor C3 is used is used to filter the DC noise that might be coupled along with the analog electrical signals.

![Schematic](https://github.com/jonathanrjpereira/LM3915-VU-Meter/tree/master/img/sch.png)

The LM386 amplifies the audio signal picked up by the microphone. The gain of the LM386 is set to 200 by connecting a 10uF capacitor between pins 1 and 8.

The LM3915 is used as the LED driver. By setting the value of resistor R4 to 4.7KΩ, the LED drive current is regulated to 3mA. A total of 20 LED's are driven by the LM3915.

The jumper connected across the header pins JP2 are used to select the display mode: Either Bar Graph mode or Moving Dot mode.

Capacitor's C1 and C2 filter out any noise in the supply line and LED1 is used to indicate the power supply status.

![Music Controlled Reactive LED Circuit Board PCB](https://github.com/jonathanrjpereira/LM3915-VU-Meter/tree/master/img/brd.png)

You can **Order the PCB:** []()

![Printable](https://github.com/jonathanrjpereira/LM3915-VU-Meter/tree/master/img/printable.png)

Or you can printout the [PDF file](https://github.com/jonathanrjpereira/LM3915-VU-Meter/tree/master/img/printable.pdf) and make your own PCB using the [Iron-on method]().

## Contributing🛠
Are you an engineer or hobbyist who has a great idea for a new feature in this project? Maybe you have a good idea for a bug fix? Feel free to grab our code & schematics from Github and tinker with it. Don't forget to smash ⭐️ & the Pull Request button.

[![alt text][1.1]][1] [![alt text][2.1]][2] [![alt text][3.1]][3]

[1.1]: https://github.com/jonathanrjpereira/Social-Media-README/blob/master/youtube.png (YouTube)
[2.1]: https://github.com/jonathanrjpereira/Social-Media-README/blob/master/instagram.png (Instagram)
[3.1]: https://github.com/jonathanrjpereira/Social-Media-README/blob/master/github.png (GitHub)

[1]: https://www.youtube.com/channel/UCRW-41O1vy98KKgJRQoYzdg
[2]: https://www.instagram.com/electroguruji/
[3]: https://github.com/jonathanrjpereira

**References:**
[LM3915 Datasheet](https://github.com/jonathanrjpereira/LM3915-VU-Meter/tree/master/img/LM3915.pdf)
[LM386 Datasheet](http://www.ti.com/lit/ds/symlink/lm386.pdf)
[Sparkfun](https://learn.sparkfun.com/tutorials/dotbar-display-driver-hookup-guide/introduction)
