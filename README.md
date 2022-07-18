# ASUS-Z690-Hackintosh-ROG-MAXIMUS-EXTREME
# ASUS ROG MAXIMUS Z690 EXTREME
![](/Images/ROGMaximusZ690Extreme.png)

# Introduction
This repository contains OpenCore EFI distributions and related files that can be used as a reference when setting up or updating your ASUS Z690 Hackintosh with the OpenCore bootloader.  The EFI is primarily based of off CaseySJ's guide for the ASUS Z690 ProArt Creator Wifi located [here](https://www.tonymacx86.com/threads/asus-z690-proart-creator-wifi-thunderbolt-4-i7-12700k-amd-rx-6800-xt.318311/) with adjustments made for the Maximus Z690 Extreme motherboard and my current setup.  This is primarily my gaming rig so just installed macOS on a separate SSD to see if it was compatible or not.

# Specifications
## Components

| Component        | Model                                | Notes |
| ---------------- | ---------------------------------------|-------------------|
| Motherboard | ASUS ROG Maximus Z690 Extreme | BIOS 1101 |
| Processor | Intel i9-12900k | |
| CPU Cooler | Corsair iCue H150i ELITE LCD Display Liquid CPU Cooler (White) | |
| RAM | 2x16 Corsair Dominator Platinum RGB DDR5 5600 Mhz (White) | |
| Boot Drive | Sabrent Rocket 1 TB | |
| Graphics Card | AMD Radeon Pro W5500 | |
| Wifi/Bluetooth Card | Broadcom BCM943602CDP |  |
| Power Supply | Corsair HX1000i | |
| Case | Lian Li PC 011 Dynamic EVO Snow White | |

## PCIe Slot Layout
| Slot | PCIe Gen | Speed | Device | Notes |
| ----- | ----- | ----- | ---------------------------------------|-------------------|
| 1 | 5 | x8 | ASUS ROG Strix RTX3090 024G GAMING | Disabled in macOS |
| 2 | 3 | x1 | Broadcom BCM943602CDP | |
| 3 | 5 | x8 | AMD Radeon Pro W5500 | |

## M.2/DIMM.2 Layout
| Slot | PCIe Gen | Device | Notes |
| ----- | ----- | ---------------------------------------|-------------------|
| M.2_1 | 5 | | |
| M.2_2 | 4 | Samsung 980 Pro 2TB | Games |
| M.2_3 | 4 | Samsung 970 EVO Plus 2 TB | Games |
| DIMM.2_1 | 4 | Samsung 970 EVO 1 TB | Windows 11 |
| DIMM.2_2 | 4 | Sabrent Rocket 1 TB | macOS |

# What Works / What Doesn't Work
- [x] Sleep / Wake
- [x] Wifi and Bluetooth
  * Disabled onboard Wifi/Bluetooth since using Broadcom BCM943602CDP card.
- [x] Handoff, Continuity, AirDrop, Continuity Camera, Universal Control, and Unlock with Apple Watch
- [x] iMessage, FaceTime, App Store, iTunes Store
- [x] 2.5G Ethernet
- [x] 10G Ethernet
- [x] HEVC, H.264
- [x] Onboard audio
  * Does not work unless you have a valid 15 port USBMap.
- [x] TRIM
- [x] USB 2.0
- [x] USB 3.2 Gen 1
- [x] USB 3.2 Gen 2
- [x] USB 3.2 Gen 2x2
- [x] Thunderbolt 4 hotplug support
    * Thunderbolt support may be hit or miss due no official support for Maple Ridge controllers in macOS
- [x] DRM
- [x] Native NVRAM
- [x] CPU Power Management
- [x] USB Power
- [ ] SideCar
    * Due to some T2 chip dependancies on MacPro7,1 and iMacPro1,1 SMBIOS



# config.plist Configuration
## PlatformInfo
You will need to create your own Serial Number and SMUUID.  Instructions can be found [here](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo).
Remember to adjust the Type to SMBIOS MacPro7,1

  Using your results from GenSMBIOS, adjust the following (replace '[Removed]') under `Generic`.

    * MLB: Board Serial
    * ROM: ROM
    * SystemSerialNumber: Serial
    * SystemUUID: SmUUID

# USB Map Configuration
The USBMap.kext file contains the full USB mapping for the ROG Maximus Z690 Extreme and has a total of 22 ports.  You will need to remove at least 7 ports so the total will be 15 or lower.

To update your usb mapping, Right-click the USBMap.kext file and click `Show Package Contents`.  Open `Info.plist` with a Plist editor like Xcode or PlistEdit Pro and navigate down to `IOKitPersonalities - MacPro7,1-XHCI - IOProviderMergeProperties - ports` as shown below.
![](/Images/USBMapplist.png)

Refer to the On-board Device diagrams below for the locations of usb mappings.  
![](/Images/motherboard.png)
![](/Images/io.png)

Once you have updated your USBMap file and removed at least 7 ports, disable `XhciPortLimit` under `Kernel-Quirks` in the config.plist.

# Changelog:
## OpenCore 0.7.8 EFI update, added onboard device diagrams with USB mappings (2022.02.15)
## Initial EFI upload, OpenCore 0.7.7 (2022.01.14)

# Credits
* [Apple](https://www.apple.com) : macOS
* [Acidanthera](https://github.com/acidanthera) : OpencorePkg, kexts, etc.
* [CaseySJ](https://www.tonymacx86.com/threads/asus-z690-proart-creator-wifi-thunderbolt-4-i7-12700k-amd-rx-6800-xt.318311/) : CaseySJ's ASUS Z690 guide
