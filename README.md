# macOS 13 Ventura on HP All-In-One 20-c081nt
### tl;dr:
* Spoof iGPU as Kaby Lake: `AAPL,ig-platform-id` = `00001659` and `device-id`= `16590000`
* Wifi/BT does not work, use wired networking for installing
* RealtekRTL8111.kext for ethernet
* SSDTs are: EC-USBX-DESKTOP, PLUG-DRTNIA, PNLF
* For sound: Set boot argument `alcid=11`
* SMBIOS is iMac18,1
* Let me know if you ever try Sonoma on similar hardware

### What works?
* Booting to macOS 13 Ventura
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
