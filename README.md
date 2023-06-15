# macOS 13 Ventura on HP All-In-One 20-c081nt
### tl;dr:
* **Spoof iGPU as Kaby Lake**: `AAPL,ig-platform-id` = `00001659` and `device-id`= `16590000`
* Wifi/BT does not work, use wired networking for installing
* RealtekRTL8111.kext for ethernet
* SSDTs are: EC-USBX-DESKTOP, PLUG-DRTNIA, PNLF
* For sound: Set boot argument `alcid=11`
* SMBIOS is iMac18,1
* Let me know if you ever try Sonoma on similar hardware

### This PC has:
* Intel Core i3-6100U
* 4 GB RAM (upped to 8 GB on mine)
* Western Digital WDC WD10EZEX-60WN4A0 1 TB HDD
* Intel HD Graphics 520
* Realtek RTL8723BE Wifi and Bluetooth Radio (unsupported)
* 1600x900 pixels onboard monitor
* UVC Compatible Camera
* Realtek RTL8168GU/8111GU Ethernet
* 4 USB ports, an Ethernet port, an HDMI port

### What works?
* Booting to macOS 13 Ventura, boot time is roughly 1 minute
* Webcam
* GPU Acceleration
* Brightness adjustment
* All USB ports
* Wired networking
* Onboard audio input and output
* Sleep and resume
* Multi-boot with Windows and Linux

### What doesn't work?
* Wifi and Bluetooth. Realtek is unsupported, there is no fix.
* Airdrop
* Showing off at subreddit because API protest

### Untested
* HDMI
* Hibernation

## Configuration
### GPU Configuration
in `config.plist`, under path `DeviceProperties/Add/PciRoot(0x0)/Pci(0x2,0x0)`
* **AAPL,ig-platform-id**: 00001659
* framebuffer-patch-enable: 01000000
* framebuffer-stolenmem: 00003001
* framebuffer-fbmem: 00009000
* **device-id**: 16590000
### Kext list, in load order
Lilu.kext
RealtekRTL8111.kext
VirtualSMC.kext
WhateverGreen.kext
AppleALC.kext
### Boot parameters
keepsyms=1 alcid=11
### SystemProductName
iMac18,1 (this will not let you update to Sonoma)
### Driver List
HfsPlus.efi -- this is required during installation. The "Method 1" mentioned in [guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/linux-install.html#downloading-macos) did not work for me.
OpenRuntime.efi
### SSDT List
SSDT-EC-USBX-DESKTOP.aml
SSDT-PLUG-DRTNIA.aml
SSDT-PNLF.aml
