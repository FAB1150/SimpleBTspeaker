# NOT TESTED YET (but it should work)
Will remove this warning once everything is tested!

# SimpleBTspeaker
Quick and dirty bluetooth speaker, using super cheap Aliexpress parts!

## Materials:
  - ESP32 DEVKIT-C (might also work with other 38 pin devboards, but check!)
  - One or two [Adafruit MAX98357A breakout boards](https://www.adafruit.com/product/3006), depending on the number of drivers
    - Dirt cheap clones can be easily found on Aliexpress!
  - Something to give the board 5V
    - Must be able to supply about 10W of power, a typical USB breakout board works
    - You can get super simple battery charging/voltage regulator modules on Aliexpress to make it portable!
  - A resistor (optional)
    - 0Ω (or a wire) bridging the "gain" contacts makes it a bit louder
    - 100KΩ makes it even louder, but it probably will shut off when playing loud music
  - Four 2.5mm pitch screw terminals (optional)
    - You can also just solder directly to the pads to make it more compact

That's it!

## Ordering the PCB:
  - Download the .zip file from the [releases tab](https://github.com/FAB1150/SimpleBTspeaker/releases)
  - Send it to your favorite pcb manufacturer :)
    - 2-layer, single PCB, 0.3mm vias. Other settings don't matter.
    - If you use JLCPCB, select "2D barcode" in "Mark on PCB".
      - On the page that pops up, select 5x5mm as the barcode size, and "specify position".

## Programming the ESP32:
  - I will upload a simple sketch soon!
    - In the meantime, you can write your own or even use the sample sketches. Here's some info:
  - Both amps are connected to the same pins (with the exception of the SD_MODE pin, which is used to select the left or right channels)
  - Pins used:
    - BCLK: GPIO 13
    - LRC: GPIO 12
    - DIN: GPIO 14
    - Pins 25 and 26 go to the MODE pin respectively of the L and R amps.
      - If you don't do anything with them, the amps will both be MONO
      - pins 25 and 26 are ADC pins, so you can analogwrite. Here's the voltage levels you want:
        - Voltage is between 0.16V and 0.77V: MONO 
        - Voltage is between 0.77V and 1.4V: RIGHT
        - Voltage is higher than 1.4V: LEFT
        - If pulled low (voltage is under 0.16V): AMP IS OFF
