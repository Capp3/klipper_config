# Klipper_config

This is my custom configuration for use with Klipper. I am includin the docs & sample config folders for easy ref in my repo.

## Klipper

<https://www.klipper3d.org/>

## The configuration for my Smoothie Clone, MKS Sbase v1.3v

<https://github.com/makerbase-mks/MKS-SBASE>

## Running on a Tevo Tarantula with a 3:1 extruder and E3D V6 Hotend

<https://e3d-online.com/products/v6-all-metal-hotend>

## Firmware information

Set the hardware to `LPC1768` when setting firmware when using the Smoothie clone

## Implimenting this

`git clone https://github.com/Capp3/klipper_config.git ~/klipper_config`

Then create a symlink for the file in the klipper config location

`ln -s ./klipper_config/tevo_sbase.cfg ./printer.cfg`

## Digging into a second MCU

Working on incorporating a RPI Pico / RP2040 as an aux mcu for accels

## The SPI Bus info

Two buses, but avilable on differnt pins. alias' are as noted in ""
"spi0a", (SPI Bus 0, Pin Set 0)
BUS_PINS_spi0a, gpio0,gpio3,gpio2, cs-gpio1
"spi0b", (SPI Bus 0, Pin Set 1)
BUS_PINS_spi0b, gpio4,gpio7,gpio6
"spi0c", (SPI Bus 0, Pin Set 2)
BUS_PINS_spi0c, gpio16,gpio19,gpio18
"spi0d", (SPI Bus 0, Pin Set 3)
BUS_PINS_spi0d, gpio20,gpio23,gpio22

"spi1a", (SPI Bus 1, Pin Set 4);
BUS_PINS_spi1a, gpio8,gpio11,gpio10
"spi1b", (SPI Bus 1, Pin Set 5);
BUS_PINS_spi1b, gpio12,gpio15,gpio14
"spi1c", (SPI Bus 1, Pin Set 6);
BUS_PINS_spi1c, gpio24,gpio27,gpio26