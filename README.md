# 3d-printer-config

## Purple voron notes

### Update klipper "firmware" on rpi

```
make menuconfig (linux process)
make clean
sudo service klipper stop
make flash
sudo service klipper start
```

### Updating klipper "firmware" on octopus

Follow: https://docs.vorondesign.com/build/software/octopus_klipper.html

Run `make menuconfig` for STM32F446 w/ 32k bootloader and 12 MHz crystal.

No need to mess with `boot0` jumper. Klipper can flip it to DFU mode.

```
make menuconfig
make clean
make
make flash FLASH_DEVICE=/dev/serial/by-id/usb-Klipper_stm32f446xx_37001A001051313133353932-if00
```

(`boot0` jumper is above logo under motor drivers.)
