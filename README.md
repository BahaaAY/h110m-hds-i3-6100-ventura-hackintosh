# Asrock H110m-hds i3-6100 Ventura Hackintosh OpenCore

[![OpenCore](https://img.shields.io/badge/OpenCore-0.9.4-blue.svg)](https://github.com/acidanthera/OpenCorePkg)
[![macOSver](https://img.shields.io/badge/macOS-13.5-brightgreen.svg)](https://support.apple.com/HT213843)

### ⚠️ Disclaimer:
- Use this EFI as a **starting point**, remember to always make your efi by following [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- This EFI may not be constantly updated to the latest version of opencore especially if no major changes are made
- Please read the whole readme before proceeding
- This readme is not yet complete and the efi is not yet complete nor clean from unused stuff
##

![ScreenShot](/Screenshots/Screenshot%201445-02-07%20at%2011.02.39%20PM.png?raw=true "ScreenShot")

### 🖥️ Hardware
| Component      | info                                                             |
|----------------|------------------------------------------------------------------|
| **CPU**        | `Intel Core i3-6100`                                             |
| **RAM**        | `Kingston 8GB 2133mhz`                                           |
| **Storage**    | `Hikvision 256GB SSD`                                            |
| **iGPU**       | `Intel UHD Graphics 530 spoofed as Intel UHD Graphics 630`       |
| **dGPU**       | `None`                                                           |
| **Audio**      | `ALC887 - alcid=1`                                               |
| **Ethernet**   | `Realtek Gigabit Ethernet RTL8111GR`                             |

### ✅️ What works</strong></summary>

- iGPU acceleration Intel UHD 530 1536 MB spoofed as Intel UHD 630
- Audio
- HDMI port
- USB ports (Using [USBInjectAll.kext](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/) Usb ports should be mapped but they are working fine for now)
- Ethernet
- iMessage
- Virtualization (Android Emulator)

### ❌️ What doesn't work

- Sleep
- Airdrop (No natively compatible wifi adapter)
- Hardware DRM (No compatible dGPU): [Fixing DRM support and iGPU performance](https://dortania.github.io/OpenCore-Post-Install/universal/drm.html)   



## ⚙️ Setup
<details>
<summary><strong>🔧 BIOS Settings</strong></summary>
  <br>


</details>
<details>
<summary><strong>🔢 Generating SMBIOS</strong></summary>
  <br>

- ### Generating SMBIOS:

Used [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) from corpnewt, to generate a fake serial number, UUID and MLB.

**This step is mandatory to get the device booting and get iServices to work later on**
1. Download GenSMBIOS from the link above as .ZIP, then extract it.
2. Start GenSMBIOS and select option `1` to download and install MacSerial
3. Select option `3` and enter `iMac18,1`
4. **IMPORTANT:** reminder that you need an **invalid serial!** to check copy and paste the second part saying `Serial: XXXXX..` in [Apple's Check Coverage Page](https://checkcoverage.apple.com/), if you get a red message saying "We're sorry, we're unable to check coverage for this serial number."
 then, you're good to go! Otherwise, go back and restart from step `2` (more info [here](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#serial-number-validity))
5. once you get the right serial number you can go and fill the generated data in the config.plist file under `PlatformInfo` section, and you are good to go! 
</details>
<details>
<summary><strong>🫣 iGPU Spoofing </strong></summary>
  <br>
  
- ### Generating Patch:
**This step is done after you finish the installation**
1. Download [Hackintool](https://github.com/benbaker76/Hackintool) and open it.
2. Go to `Patch` Category 
3. Select `Kaby Lake` in the `Intel Generation` Dropdown.
4. Select `0x59120000` in the `Platform ID` Dropdown.
5. Go to the `Patch` Tab and the `Advanced` menu.
6. Enable `DP -> HDMI`, `Use Intel HDMI`, and `Enable HDMI20 (4K)`.
7. Enable `Spoof Video Device ID` and select `0x5912: Intel HD Graphics 630` from the dropdown menu.
8. Click `Generate Patch`
9. Now you got the patch, you need to copy the `PciRoot(0x0)/Pci(0x2,0x0)` Key .
10. Paste it under `DeviceProperties > Add` in your config.plist file.
11. Enjoy!

</details>





  
## not completed yet...
