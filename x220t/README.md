# x220t Coreboot

This folder contains files, blobs and some text about the building and flashing Coreboot on my x220t.

Original RAW files are stored in the `original` folder.

As for now the original BIOS is in the file `flash.bin`. If you want to reset to the original BIOS please use a backup from original to make sure, you are restoring REALLY a original BIOS.

## Flash and Image files

* flash.bin - Original BIOS image
* gbe.bin - Gigabit Ethernet blob
* vgabios.bin Extracted VGA section from flash.bin using the UEFITool

## Builds

All current builds for MY x220t are in the builds folder. Currently there is

* coreboot_gbe_nativevga.rom - Coreboot build with gbe and nativevga.rom

## Documentation

Currently very sparse and distributed accross mutliple machines, in the wiki, as a gist and here.

I will work on that soon!
