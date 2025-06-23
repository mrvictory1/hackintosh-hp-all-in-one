# macOS 15 Sequoia on HP All-In-One 20-c081nt
### tl;dr:
* **Spoof iGPU as Kaby Lake**: `AAPL,ig-platform-id` = `00001659` and `device-id`= `16590000`
* **Set con1 to HDMI**: `framebuffer-con1-enable` = `01000000` and `framebuffer-con1-type` = `00080000`
* Use v2.4.2 of RealtekRTL8111.kext instead of latest version
* HDMI monitor must be unplugged at boot, it can be plugged in at login screen if there is one
* Wi-Fi/BT do not work, use wired networking for installing
* RealtekRTL8111.kext for ethernet
* SSDTs are: EC-USBX-DESKTOP, PLUG-DRTNIA, PNLF
* For sound: Set boot argument `alcid=11`
* SMBIOS is iMac19,1
* iMac19,1 does not support Tahoe, iMac20,1 supports Tahoe but is untested on this hardware

### This PC has:
* Intel Core i3-6100U
* 4 GB RAM (upgraded to 8 GB on mine)
* Western Digital WDC WD10EZEX-60WN4A0 1 TB HDD
* Intel HD Graphics 520
* Realtek RTL8723BE Wifi and Bluetooth Radio (unsupported)
* 1600x900 pixels onboard monitor
* UVC Compatible Camera
* Realtek RTL8168GU/8111GU Ethernet
* 4 USB ports, an Ethernet port, an HDMI port

### What works?
* Booting to macOS 15 Sequoia, boot time is roughly 1 minute
* Webcam
* GPU Acceleration
* Brightness adjustment
* All USB ports
* Wired networking
* Onboard audio input and output
* HDMI video & audio output
* Sleep and resume
* Multi-boot with Windows and Linux

### What doesn't work?
* Wi-Fi and Bluetooth. Realtek is unsupported, there is no fix.
* FairPlay 1.x, black screen on test video.

### Untested
* Hibernation
* FairPlay 4.x

## Configuration
### GPU Configuration
in `config.plist`, under path `DeviceProperties/Add/PciRoot(0x0)/Pci(0x2,0x0)`
* **AAPL,ig-platform-id**: 00001659
* framebuffer-patch-enable: 01000000
* framebuffer-stolenmem: 00003001
* framebuffer-fbmem: 00009000
* **device-id**: 16590000
* **framebuffer-con1-enable**: 01000000
* **framebuffer-con1-type**: 00080000
### Kext list, in load order
* Lilu.kext
* RealtekRTL8111.kext (version 2.4.2)
* VirtualSMC.kext
* WhateverGreen.kext
* AppleALC.kext
### Boot parameters
keepsyms=1 alcid=11
### SystemProductName
iMac19,1 (this will not let you update to Tahoe)
### Driver List
* HfsPlus.efi -- this is required during installation. The "Method 1" mentioned in [guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/linux-install.html#downloading-macos) did not work for me.
* OpenRuntime.efi
### SSDT List
* SSDT-EC-USBX-DESKTOP.aml
* SSDT-PLUG-DRTNIA.aml
* SSDT-PNLF.aml
### Installation & Boot
* Before installation, in `config.plist`, under path `Misc/Security/SecureBootModel` set `SecureBootModel` to `Disabled`. This setting can be reverted after installation is complete.
* HDMI monitor must be unplugged at boot. If it is plugged, internal display will stop working and external display will be unusably slow until reboot. Reconnect it after login screen appears.
