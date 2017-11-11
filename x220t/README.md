# x220t Coreboot

This folder contains files, blobs and some text about the building and flashing Coreboot on my x220t.

Original RAW files are stored in the `original` folder.

As for now the original BIOS is in the file `flash.bin`. If you want to reset to the original BIOS please use a backup from original to make sure, you are restoring REALLY a original BIOS.

## Flash and Image files

* `flash.bin` - Original BIOS image
* `gbe.bin` - Gigabit Ethernet blob
* `vgabios.bin` Extracted VGA section from flash.bin using the [UEFITool](https://github.com/LongSoft/UEFITool)

## Builds

The current working build is `coreboot-20171108.bin` and stored here.

# Instructions

These instructions are done myself based on the official instructions from the Wiki and multiple pages.
It was working for my device but may need some fine-tuning for yours in order to make it work.

First: The device **could potentially be destroyed!** Make sure you can afford the loss.

## Preparations

You will need the following tools

* Laptop (x220 or x220t, I am working on the x220t based on the instructions for the x220, so that one should work fine)
* Screwdrivers
* Raspberry Pi 3 Model B
* USB to TTY Serial Cable
* Pomona SOIC8 5250 Test Clip
* 8x Female Jumper Wire
* HDMI cable, external monitor and external keyboard for the Raspberry
* (Optional but highly recommended) - Second computer, where you will build coreboot.

In principle you can also build the stuff on the Raspberry, but that might take a while.

## Disassemling the X220t

First: Power down the Laptop and remove the battery. **THIS IS CRITICAL**
Not removing the power is acutally the only thing where you can screw up really bad! Having the mainboard powered while flashing the BIOS could burn it. Make sure this is done properly!!

Remove the Keyboard and the Palmrest. It works straightforward but if you're unsure, read the Lenovo Guide [https://support.lenovo.com/us/en/videos/pd022683].

I skip this part for now, because other people have documented this pretty well themselves. See for example [https://tylercipriani.com/blog/2016/11/13/coreboot-on-the-thinkpad-x220-with-a-raspberry-pi/]


