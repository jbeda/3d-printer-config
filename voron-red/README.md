# voron-red

## Update klipper "firmware" on rpi

```
make menuconfig (linux process)
make clean
sudo service klipper stop
make flash
sudo service klipper start
```

## Important Numbers/links

LDO Leviathan Setup docs: https://ldomotion.com/p/guide/VORON-Leviathan-V12
CAN on bullseye:
Birds' Nest UUID: c1058a179bbc
Toolhead 0 (EBB36) CANbus UUID: 829b3f4becec
Toolhead 1 (EBB36) CANbus UUID: e31d84775fe2

## Klipper Update

```bash
sudo service klipper stop
cd ~/klipper
git pull

# Leviathan
make clean KCONFIG_CONFIG=config.leviathan
make menuconfig KCONFIG_CONFIG=config.leviathan
make KCONFIG_CONFIG=config.leviathan
~/katapult-env/bin/python3 ~/katapult/scripts/flashtool.py -d /dev/serial/by-id/usb-Klipper_stm32f446xx_3B0040000251303532383235-if00 -f out/klipper.bin

# Bird's Nest CAN
make clean KCONFIG_CONFIG=config.birdsnest
make menuconfig KCONFIG_CONFIG=config.birdsnest
make KCONFIG_CONFIG=config.birdsnest
~/katapult-env/bin/python3 ~/katapult/scripts/flashtool.py -i can0 -r -u c1058a179bbc
~/katapult-env/bin/python3 ~/katapult/scripts/flashtool.py -d /dev/serial/by-id/usb-katapult_stm32g0b1xx_0A00300011504D5930313920-if00 -f out/klipper.bin

# Toolheads
make clean KCONFIG_CONFIG=config.toolhead
make menuconfig KCONFIG_CONFIG=config.toolhead
make KCONFIG_CONFIG=config.toolhead

# Toolhead 0
~/katapult-env/bin/python3 ~/katapult/scripts/flashtool.py -i can0 -f out/klipper.bin -u 829b3f4becec
# Toolhead 1
~/katapult-env/bin/python3 ~/katapult/scripts/flashtool.py -i can0 -f out/klipper.bin -u e31d84775fe2

sudo service klipper start
```

## Mods

- LDO Voron 2.4 kit, rev D
- [Chaoticlab Voron 2.4 CNC Parts Kit
  v2.0](https://www.chaoticlab.com/products/voron-2-4-cnc-parts-kit-v2-0?variant=40839644905570)
- [BTT HDMI5 v1.2
  screen](https://biqu.equipment/products/bigtreetech-hdmi5-v1-0-hdmi7-v1-0?variant=39984058105954).
  For some reason the screen included in the LDO kit had phantom inputs. I
  consider that dangerous.
  - [Mount for BTT HDMI5
    screen](https://www.printables.com/model/1066444-btt-hdmi5-mount-for-the-clicky-clack-fridge-door-w/files)
    with [this
    part](https://www.printables.com/model/926845-btt-hdmi5-v12-display-mount-voron)
    for v1.2.
- [Annex Panel
  Clips](https://github.com/Annex-Engineering/Annex-Engineering_User_Mods/tree/main/Printers/All_Printers/annex_dev-Panel_2020_Clips_and_Hinges)
- [Clicky Clack Fridge
  Door](https://github.com/tanaes/whopping_Voron_mods/tree/main/clickyclacky_door)
  with [DraftShift DoorBuffer](https://github.com/DraftShift/DoorBuffer).
- Extrusion based top hat using Clicky Clack hinges. BOM:
  - 4x Mitsumi HFSB5-2020-250 (Cross drilled on both ends. I did it myself but Mitsumi
    can do it with -LCP code)
  - 8x Mitsumi HFSB5-2020-420 (Tapped on both ends. I did it myself but Mitsumi
    can do it with -TPW code)
  - Edge strip. 6x10mm, 10 meters from
    [AliExpress](https://www.aliexpress.us/item/3256802603648215.html)
  - 4x 3mm Acrylic panels. 218mmx428mm
- [StealthChanger](https://github.com/DraftShift/StealthChanger)
- 1 (eventually 4) [Dragon
  Burner](https://github.com/chirpy2605/voron/tree/main/V0/Dragon_Burner)
  toolheads
  - Revo Voron hotend w/ 60W heater
  - [Galileo 2
    Standalone](https://github.com/JaredC01/Galileo2/tree/main/galileo2_standalone)
    extruder
  - [BTT EBB36 CAN
    v1.2](<https://github.com/bigtreetech/EBB/tree/master/EBB%20CAN%20V1.1%20and%20V1.2%20(STM32G0B1)>)
    toolhead board
  - [Orbiter V2 BTT EBB36
    carrier](https://github.com/DraftShift/StealthChanger/blob/main/UserMods/onsimon/README.md)
    toolhead board carrier
  - [Custom EBB36 G2SA PG7
    mount](https://cad.onshape.com/documents/bd81efa30bd02efa40c9785e/w/b6631380ec4d6ba2076ef068/e/de1d270a613df399ea0e3da1)
    somewhat inspired by [this model](https://www.printables.com/model/791804-ebb36-mount-for-orbiter-2-and-pg7-gland-optimized/related)
  - Magnetic Dock version of Dragon Burner on [DraftShift Discord](https://discord.com/channels/1226846451028725821/1320029517376655462/1347878802751230005)
- [FannyPack](https://github.com/DraftShift/CableManagement/tree/main/FannyPack)
  for cable management with
  [N3MI-DG](https://github.com/DraftShift/CableManagement/tree/main/UserMods/N3MI-DG/Umbilical_plates_V2)
  umbilical plates. TPU based with spring steel support
- [Igus CF113-018-D](https://www.igus.com/product/CF113_D?artnr=CF113-018-D) for
  CAN to/from toolheads along with power. This has 2x(2x24 AWG) and 2x20 AWG
  - red/black (24AWG) - CAN low/high to toolhead
  - grey/pink (24AWG) - CAN low/high from toolhead
  - white/brown (20AWG) - +/- 24v
- [Birds' Nest CAN board](https://github.com/xbst/Birds-Nest-CAN).
- Chamber Thermistor. [Generic
  3950](https://www.amazon.com/gp/product/B07D9LSKWK/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
  [mounted to back of
  gantry](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/samwiseg0/extrusion_thermistor_mount).

Purchased but not used:

- [Igus CF9-05-04 cable](https://www.igus.com/product/CF9?artnr=CF9-05-04) for
  CAN and power to toolheads. This is 4x20awg cable.
  - white - +24v
  - brown - ground
  - green - CAN low
  - yellow - CAN high
- [BTT CEB v1.0](https://github.com/bigtreetech/CEB) CAN distribution board.
