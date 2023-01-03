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

### RPi Pico Hardware info

#### SPI Bus info

Two buses, but avilable on differnt pins. alias are as diffined in Klipper

| Bus     | Alias | RX/MISO | TX/MOSI | SCK    | CS     |
| ------- | ----- | ------- | ------- | ------ | ------ |
| SPI0/0  | spi0a | gpio0   | gpio3   | gpio2  | gpio1  |
| SPI0/1  | spi0b | gpio4   | gpio7   | gpio6  | gpio5  |
| SPI0/2  | spi0c | gpio16  | gpio19  | gpio18 | gpio17 |
| SPI0/3* | spi0d | gpio20  | gpio23  | gpio22 |        |
| ------- | ----- | ------- | ------- | ------ | ------ |
| SPI1/4  | spi1a | gpio8   | gpio11  | gpio10 | gpio9  |
| SPI1/5  | spi1b | gpio12  | gpio15  | gpio14 | gpio13 |
| SPI1/6* | spi1c | gpio24  | gpio27  | gpio26 |        |

*- Pins are defined in the Klipper Code, but not marked on most Pico pinouts

#### Pico Firmware

Go to Klipper Directory and create firmware

`cd ~/klipper/

Clear old firmwares

```
make clear
```

Then setup the firmware

```
make menuconfig
make
```

##### Flashing Firmware

Given no other drive are attqached, the Pico should register as block device 
`/dev/sda
Mount the block device and copy the Klipper firmware file to it

```
sudo mount /dev/sda1 /mnt
sudo cp out/klipper.uf2 /mnt
sudo umount /mnt
```

After un-mounting, the Pico should automatically reboot with the new firmware
