# voron-purple

## Update klipper "firmware" on rpi

```
make menuconfig (linux process)
make clean
sudo service klipper stop
make flash
sudo service klipper start
```

## Updating klipper "firmware" on octopus

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

## Mods

- LDO Voron v2.4 kit, rev B
- Revo hotend with 60w heater and high flow nozzles
- [Purge Bucket and
  brush](https://github.com/VoronDesign/VoronUsers/tree/main/orphaned_mods/edwardyeeks/Decontaminator_Purge_Bucket_%26_Nozzle_Scrubber)
- [Nevermore v5 Duo](https://github.com/nevermore3d/Nevermore_Micro)
- [LED bar
  clips](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/eddie/LED_Bar_Clip)
- [Beefy Front Idlers](https://github.com/clee/VoronBFI)
- [5" touch
  screen](https://www.fabreeko.com/products/raspberry-pi-5-inch-touch-screen-ips-800x480-by-fysetc)
  with [Display
  Mount](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/Tircown/Display_mount_5inch)
  - Mount: [45
    Degree](https://www.printables.com/model/869887-voron-24-btt-pitft50-45-degree-mount-clicky-clack)
    and [display
    holder](https://www.printables.com/model/311396-tft-5-holder-for-voron-24-btt-20-pitft50/files).
    These aren't exactly the right thing for this screen but it seems to work
    just fine.
- [Tap](https://github.com/VoronDesign/Voron-Tap)
- [Chaoticlab CNC Tap](https://www.chaoticlab.com/products/cnc-voron-tap)
  - [X Endstop Trigger](https://www.printables.com/model/703550-chaotic-labs-cnc-tap-v2-x-endstop-trigger)
- [Galileo 2](https://github.com/JaredC01/Galileo2)
- [GE5C Z
  joint](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/hartk1213/Voron2.4_GE5C)
- CAN bus with BTT SB2209 (RPI 2040 version) and BTT U2C v2.1 routed through
  cable chains. Harness from https://kb-3d.com/.
- Chamber Thermistor. [Generic
  3950](https://www.amazon.com/gp/product/B07D9LSKWK/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
  [mounted to back of
  gantry](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/samwiseg0/extrusion_thermistor_mount).
- [Snap
  Latches](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/richardjm/snap-latch-2020)
- [Clicky Clack Fridge Door](https://github.com/tanaes/whopping_Voron_mods/tree/main/clickyclacky_door)
- Logitech C920 with
  [mount](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/PsychoShaft/C92X_PsycHoShafts_Mount)
- [BTT Smart Filament Sensor
  v2](https://biqu.equipment/products/btt-sfs-v2-0-smart-filament-sensor)
  - [BTT SFS v2 backpanel
    mount](https://www.printables.com/model/566269-btt-sfs-smart-filament-sensor-v20-voron-backpanel-)
