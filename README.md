# Klipper_config

This is my custom configuration for use with Klipper. I am includin the docs & sample config folders for easy ref in my repo.

## Klipper

<https://www.klipper3d.org/>

## The configuration for my Smoothie Clone, MKS Sbase v1.3v

<https://github.com/makerbase-mks/MKS-SBASE>

## Running on a Tevo Tarantula with a 3:1 extruder and E3D V6 Hotend

<https://e3d-online.com/products/v6-all-metal-hotend>

# Firmware information

Set the hardware to `LPC1769` when setting firmware when using the Smoothie clone

# Implimenting this

`git clone https://github.com/Capp3/klipper_config.git ~/klipper_config`

Then create a symlink for the file in the klipper config location

`ln -s ./klipper_config/tevo_sbase.cfg ./printer.cfg`