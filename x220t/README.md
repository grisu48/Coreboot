# x220t Coreboot

This folder contains files, blobs and some text about the building and flashing Coreboot on my x220t.

Original RAW files are stored in the `original` folder.

As for now the original BIOS is in the file `flash.bin`. If you want to reset to the original BIOS please use a backup from original to make sure, you are restoring REALLY a original BIOS.

## Flash and Image files

* `flash.bin` - Original BIOS image
* `gbe.bin` - Gigabit Ethernet blob
* `vgabios.bin` Extracted VGA section from flash.bin using the [UEFITool](https://github.com/LongSoft/UEFITool)

## Builds

The current working build is `coreboot-20180527.bin` (Coreboot 4.8)

The status of the builds is

* `coreboot-20180527.bin` ***(Current)*** - Tested, OK
* `coreboot-20180502.bin` - Tested, OK
* `coreboot-20171108.bin` - Tested, OK

### coreboot-20180527.bin

This is the current build, based on Coreboot 4.8 (Commit 98376b84592aea85089f047957c39b3889136574)

Tested on my x220t, works fine. One issue still needs investigation: if the `intel_idle.max_cstate=1` is still required.

### coreboot-20180502.bin

This is the current build, based on Coreboot 4.7.

This build is a bit picky about the memory bars, I had to unplug and re-plug them and in general has some weird issues from time to time. Take the `coreboot-20180527.bin` build instead.

### coreboot-20171108.bin

First build, works fine. If you expect (like me) random complete system freezes from time to time, consider disabling higher sleeping C-state of the CPU by adding the following to the kernel parameters

    intel_idle.max_cstate=1

See [Random freezes](#Random-freezes) for more details

## Known issues

### Random freezes

If you are expecting random freezes, this could come from the intel CPU, that hangs in a higher C-state.

Solution: add `intel_idle.max_cstate=1` to the kernel parameters

    # in /etc/defaults/grub
    GRUB_CMDLINE_LINUX_DEFAULTS="intel_idle.max_cstate=1"

That solved the issue for me

Other approaches are documented at https://bbs.archlinux.org/viewtopic.php?id=220716

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

# Update

You can re-follow the procedure above, or you use `flashrom` to update an already with Coreboot flashed laptop.

## Flashrom

In a nutshell

    # Boot kernel with 'iomem=relaxed'
    # As superuser:
    flashrom -p internal:laptop=force_I_want_a_brick -c "CHIPNAME" -w BINARY

For now I don't recall the `CHIPNAME`, but it was the most simple one when getting the list with `flashrom -p internal:laptop=force_I_want_a_brick`.

    # Get list of available chips
    sudo flashrom -p internal:laptop=force_I_want_a_brick

On my x220t `CHIPNAME` is `MX25L6405`

### Strict DevMem

As of Kernel 4.4, `CONFIG_IO_STRICT_DEVMEM` is a new security measure than can make flashrom stop working. In that case add `iomem=relaxed` to your kernel parameters (https://wiki.archlinux.org/index.php/Flashing_BIOS_from_Linux#Usage)

### Weblinks 

* https://wiki.archlinux.org/index.php/Flashing_BIOS_from_Linux

