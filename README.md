# cromix-emu

A software emulation of Cromemco hardware to run Cromix Plus.

Usage: java -jar s100-68k-emu-1.2.jar -configfile ./Cromix-cromemco.yaml -g

## Release 1.2
* Requires Java 17 runtime
* Configurable terminal font size and style
* Inbuilt telnet server provides remote console capability
* Defect fixes

### Font size and style
The font size and style for the inbuilt console terminal can be configured using the console.fontSize and console.fontName properties in the configuration file.

### Telnet server
The telnet server can be used inplace of the inbuilt console terminal to provide a remote console.  To enable telnet, change the console.type property in the configuration file to **telnet**.  By default the telnet server listens on port 2020 at address 127.0.0.1.  For remote capability change the listening address (property console.address) to **0.0.0.0**.  
Cromix expects the Enter key to send 0xd (ctrl-M), this is not the default in some Windows telnet client software such as putty.

**Note:** 
* The included ST image is based on version 162 , it has been discovered that some programs, such as **find**, still require the Z80 CPU.  Therefore, these programs will crash the emulator.  An updated ST image will be included in a later release.
* Refer to previous release notes for other details.

## Release 1.1
* Requires Java 17 runtime
* Minimal UI for 64FDC and STDC
* Boots from IMD floppy images (large only)
* Boots from partitioned ST images

### UI
The UI displays the current status and activity for the 64FDC and STDC drives.  
The 64FDC drives can be ejected and loaded.

![UI Image](emu-ui.png)

Note: The emulator loads and operates on the 64FDC and STDC disk images in memory, changes to the disk image files are not automatically persisted to disk.  You must use the Sync buttons to persist any changes.

The info icons display the STDC disk parameters and partition table.

![UI Image](emu-ui-info.png)

### Boot device

The default boot device is configured in the boot section of the config file which is in yaml format, https://yaml.org/spec/1.2.2.

Whilst running, the boot device can be changed and the emulation rebooted via the UI.

#### Boot section
![Boot Image](emu-ui-boot.png)

* **board:** Can be either "Cromemco 64FDC" or "Cromemco STDC"
* **device:** The index of the device: 0,1,2,3 for the 64FDC or 0,1 for the STDC
* **unit:** Ignored for the 64FDC, the partition index for the STDC

### Using Gesswein MFM emulator HDD files
The .hdd file must be converted to a raw image file using the mfm_util utility, https://github.com/dgesswein/mfm.git

`mfm_util --emulation_file 20220705.D45.C1536.H16.master.hdd --extracted_data_file 20220705.D45.C1536.H16.master.img -a`

# Previous releases
## Release 1.0

Requires Java 8 (minimum) runtime

Usage: java -jar s100-68k-emu-1.0.jar -configfile ./Cromix-cromemco.yaml -g

![Boot Image](emu-boot.png)
