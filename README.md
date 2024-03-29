# Klipper_config

This is my custom configuration for use with Klipper. I am includin the docs & sample config folders for easy ref in my repo.

## Klipper

<https://www.klipper3d.org/>

## The configuration for my Smoothie Clone, MKS Sbase v1.3v

<https://github.com/makerbase-mks/MKS-SBASE>

## Running on a Tevo Tarantula with a 3:1 extruder and E3D V6 Hotend

<https://e3d-online.com/products/v6-all-metal-hotend>

## MCU Physical Connection

MCUs connected, and flashed, will be findable using;
`ll /dev/serial/by-id/*`

## Firmware information

Set the hardware to `LPC1769` when setting firmware when using the Smoothie clone

## Implimenting this

`git clone https://github.com/Capp3/klipper_config.git ~/klipper_config`

Then create a symlink for the file in the klipper config location

`ln -s ./klipper_config/tevo_sbase.cfg ./printer.cfg`

`ln -s ./klipper_config/my_macros.cfg ./my_macros.cfg`

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

#### i2c Bus info

In an attempt to get a BMP280 temp sensor to work.

Not sure about using i2c and SPI at the same time. 

| Alias | SDA    | SCL   |
| ----- | -----  | ----- |
| i2c0a | gpio0  | gpio1 |
| i2c0b | gpio4  | gpio5 |
| i2c0c | gpio8  | gpio9 |
| i2c0d | gpio12 | gpio13 |
| i2c0e | gpio16 | gpio17 |
| i2c0f | gpio20 | gpio21 |
| i2c0g | gpio24 | gpio25 |
| i2c0h | gpio28 | gpio29 |
| i2c1a | gpio2  | gpio3 |
| i2c1b | gpio6  | gpio7 |
| i2c1c | gpio10 | gpio11 |
| i2c1d | gpio14 | gpio15 |
| i2c1e | gpio18 | gpio19 |
| i2c1f | gpio22 | gpio23 |
| i2c1g | gpio26 | gpio27 |

#### Pico Firmware

Go to Klipper Directory and create firmware

```
cd ~/klipper/
```

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

Given no other drive are attached, the Pico should register as block device 
`/dev/sda
Mount the block device and copy the Klipper firmware file to it

```
sudo mount /dev/sda1 /mnt
sudo cp out/klipper.uf2 /mnt
sudo umount /mnt
```

After un-mounting, the Pico should automatically reboot with the new firmware

##### Pico (RP2040) Reseting issue

RP2040s reseting is messed up in klipper, use the below to correct

###### Workaround to connect rp2040 on startup or reboot

SSH to the klipper host 

```bash
sudo apt install uhubctl -y
sudo nano /etc/rc.local
```

Insert this text before `exit 0`

```bash
uhubctl -l 1-1 -a 2
sleep 1 && uhubctl -l 1-1 -a 2
```

## Mainsail

### USB Webcam

#### Before you do all the stuff below, try linking the klipper_config directory in this repository to the Mainsail Klipper Config Dir

`ln -s ./klipper_config/ ~/klipper_config`

#### Or do all this

Need  to locate camera "long name" with
`ll  /dev/v4l/by-id/`

Then edit `/home/pi/klipper_config/webcam.txt` and add:

```txt
camera="usb"
camera_usb_options="-r 640x480 -f 10 -d /dev/v4l/by-id/usb-046d_Logitech_Webcam_C930e_C88D4AEE-video-index0
```
