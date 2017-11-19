# Operating the GU20X8 Display with Arduino

The [GU20X8](gu20x8.md) display can be operated using an Arduino or equivalent micro controller.

## Directly Connected

The parallel interface can be connected to digital pins of the Arduino directly.

The minimal configuration includes the address bus (6 pins), the data bus (8 pins), and the write control pin WR, so summing up to 15 pins.

For fast but safe timing, your micro controller should care about the signal from the BUSY pin.
If you wish to control the brightness, you also need the C/D pin connected instead of wired to 5V.
If you wish to enable/disable the display without clearing the display buffer, or hiding random pixel pattern at startup, you need the EN pin controllable instead of wired to 5V.
If you even wish to reset the display from the micro controller, you need the RST pin.

This will result in 15 to 19 pins. What is quite a lot, but it is still possible with the Arduino Nano (no idea about the other models).
However, this makes it difficult to add other devices, as the Arduino will run out of pins.

A library with an example can be found on my GitHub project [GU20X8Lib](https://github.com/cawapy/GU20X8Lib).
The example sketch uses the pin assignment as depicted [in this fritzing file](Direct-Connected-Example.fzz).

## Using Shift Registers

Instead of connecting the pins directly to the Arduino, you can also use shift registers, such as the well known HC595.
Typically, shift registers have 8 output pins, but can be cascaded.
The output pins of the shift registers will control the input pins of the display.

So 2-3 of such registers will be sufficient, depending on how many input pins of the display you want to control.
The BUSY pin of the display is output, so this still needs to be connected to the Arduino directly.

And the shift register cascade also needs to be controlled by the Arduino, typically requiring at least 3 pins.
They can be even controlled using the SPI bus.

While this option requires more components and also software adaptions, you'll have more pins left for other purposes.

