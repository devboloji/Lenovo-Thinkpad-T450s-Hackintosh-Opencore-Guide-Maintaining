# Lenovo-Thinkpad-T450-T450s-Hackintosh-Guide-Opencore
This repo contains the installation guide and EFI files required to get a perfectly functional Catalina and Big Sur Hackintosh on your Brodwell (5th gen) T450 or T450s. Everything is stable and functional as described in the Readme.
<hr>

# Lenovo Thinkpad T450 & T450s Hackintosh Guide for Catalina, Big Sur with OpenCore
This repo contains the installation guide and EFI files required to get a perfectly functional  Catalina, Big Sur, Monterey hackintosh on your T450 or T450s since they share the same hardware. Everything is stable and functional as described in this Readme. 

## A few worthy mentions about this repo:

- **This guide is not for models with Haswell 4th gen CPU**
- **The patched ACPI files were first created by [EchoEspirit](https://github.com/EchoEsprit/Hackintosh-Catalina-OpenCore-Lenovo-T450s-efi). Then [racka98](https://github.com/racka98/Lenovo-Thinkpad-T450-T450s-Hackintosh-Guide-Opencore) Tweaked couple of things and fixed some errors and Released for some months to opencore 0.7.0. Later I tweaked couple of things and Updated the Release of 0.7.0 to 0.8.2.**
- **I will try my best to keep the repo updated with the latest kexts and OpenCore version**
- **This EFI works with ,MacOS Big Sur, Catalina (Need to tweak some of the things to work perfectly.**
-**For macOS Monterey this EFI will work great as BigSur, But audio is not working Only in Monterey. Tried many ways to fix but may fix later releases. so don't expect flawless functionality**
- **This EFI is Configured with Big Sur in mind. If you are using it on Monterey, Catalina read the the whole guide to know where to make the necessary changes**
- **With every EFI update you retrieve from here please remember to go through the post install guide**
<hr>

![img](https://img.shields.io/badge/Release%20Update-July-red) ![img](https://img.shields.io/badge/macOS%20Support-BigSur--11.6.7-blue)![img](https://img.shields.io/badge/macOS%20Support-Catalina-blue) ![img](https://img.shields.io/badge/OpenCore%20Version-0.8.2-yellow)


# Introduction

EFI folder and Guide for Thinkpad T450 and T450s Hackintosh BigSur.

- `Tested CPUs`: **i7-5600u**(not tested in i5-5200U/5300u, If anyone tested, Let me know: [facebook](https://www.facebook.com/sai.dev.92317) and [telegram](https://t.me/Pappusaidev))
- `Integrated Graphics`: **HD Graphics 5500**
- `Sound Card`: **ALC292**
- `Wireless Cards Tested`: **Intel 7265/7260**(not tested in DW1820A 00JT494/Broadcom BCM94360CSAX)s
<hr>

# What works

- Sleep / Wake
- Wifi and Bluetooth (Intel® Dual Band Wireless-AC 7265 or 7260 cards with Airportitlwm.kext) **(Note: the intel kexts for wifi and bluetooth come with some issues, see post install notes for more info, new Airportitlwm Monterey kext & fixes)**
- AirPort Extreme (Broadcom BCM94360CSAX & NGFF A/E Adapter) **Recommended Upgrade to get native WiFi & Bluetooth**
- Handoff, Continuity, AirDrop
- iMessage, FaceTime, App Store, iTunes Store (see Opencore post install guide for more info)
- Ethernet
- Onboard audio (see post install guide for more info)
- USB 2.0 / USB 3.0
- Dual Batteries
- Touchpad
- Trackpoint
- miniDP
- SD Card Reader (Enable Sinetek-rtsx.kext in Config.plist because it is unstable to be left on by default)
- HiDPI (Use [one-key-hidpi](https://github.com/xzhih/one-key-hidpi))
- Sidecar (see post install guide for more info)

# What doesn't work
- Fingerprint
- VGA
- Headphones

## Note: If you need to edit Config.plist, don't Clover configurator because its opencore. Use OpenCore configurator , use PlistEdit pro, PropperTree, or Xcode.

# Setting Up Bios

- `Security -> Security Chip`: **Disabled**;
- `Memory Protection -> Execution Prevention`: **Enabled**;
- `Virtualization -> Intel Virtualization Technology`: **Enabled**;
- `Virtualization -> Vt-directed IO`: **Disabled**;
- `Internal Device Access -> Bottom Cover Tamper Detection`: must be **Disabled**;
- `Anti-Theft -> Computrace -> Current Setting`: **Disabled**;
- `Secure Boot -> Secure Boot`: **Disabled**;
- `UEFI/Legacy Boot`: **UEFI Only**;
- `Fingerprint Sensor`: **Disabled** `(Causes issues with wake from sleep)`;
- `CSM Support`: **Yes**.
<hr>

# Installation Guide (Online Installer Reccomended)
## Gibmacos installation process may not work for this EFI(I didn't test this process for this release of efi)but you can try.
## macOS Bigsur Online Installer with Windows:
**This is a simple and quick summary of the online install USB creation**

Windows Guide:(Works for Macos users also)

1. Download [rufus](https://rufus.ie/en/)
2. Select the desired flash drive or Sdcard you would like to put the installer on under the device option
3. Select `non-bootable` as the boot selection (REQUIRED)
4. Select `FAT-32` or `Large FAT-32` as the partition scheme
- `For mac users`
1. Launch Disk Utility
2. `Select View` > `Show all devices` at the top left
3. Select your flash drive (root usb device)and format it as `MS-DOS (FAT)` or `FAT-32`
and change `guid patition table`-> `Master Boot Record Partiton`.
5. Open up the usb partition in file explorer and delete the files created by rufus
6. Create a folder on that partiton named `com.apple.recovery.boot`
7. Install Python from Microsoft store or Download manually here -> [python](https://www.python.org/downloads/) (Make sure you select add python x.x to path)
8. Download and extract the [OpenCore Package](https://github.com/acidanthera/OpenCorePkg/releases)
9. Select the macrecovery folder in the opencorepkg folder at `/Utilities/macrecovery/`
10. Click on home > copy path at the top of file explorer
11. Fire up command prompt and type `cd` and hit spacebar and paste the path of the macrecovery folder.
12. Run the command `macrecovery.py -b Mac-42FD25EABCABB274 -m 00000000000000000 download`
13. This will put some files in the macrecovery folder but we only need BaseSystem.dmg and BaseSystem.chunklist (takes approx. 600mb to 800mb internet)for Downloading the Macos installer.
14. Paste both of those files in the `com.apple.recovery.boot` folder in your flash drive partiton
15. Download the latest EFI created [here](https://github.com/devboloji/Lenovo-Thinkpad-T450-T450s-Hackintosh-Guide-Opencore/releases)
16. Copy the EFI folder and paste it in your USB partiton.
- ### Note: IF YOU ARE USING THE CATALINA, THEN YOU NEED TO EDIT ONE THING IN CONFIG ->> open `config.plist`->`Misc`->`Security`-> `SecureBootModel`->TYPE `Disabled`.

`Note: Make sure to apply the correct bios settings before continuing (provided above)`

17. Restart your laptop and hit `F12`
18. Select your flash drive as temporary boot option
19. Now in the OpenCore menu select the name of your USB partiton
Great! Now install and set up macOS Big Sur as usual(This process will be required 14gb internet to download full Macos bigsur). When you are done be sure to read my post install guide.

 # MacOS BigSur Offline Installer from Windows and Macos:
 
- 1.Search and Download Olarila BigSur .raw from [Here](https://www.olarila.com/topic/6278-hackintosh-and-macintosh-olarila-vanilla-images-macos/)the latest version of bigsur is 11.6.7
- 2.Download etcher from [here](https://www.balena.io/etcher/)
- 3.Make Usb bootable (Flash the Sdcard) using Etcher and olarila bigsur.
- 4.mount the efi of Sdcard or bootable drive.You can watch about mounting the efi in windows[Youtube](https://www.youtube.com/watch?v=-XwKjS6hbwQ) just watch how to select the olarila image from the website and mounting the efi 
- For mac users use opencoreconfigurator official [here](https://mackie100projects.altervista.org/download-opencore-configurator/)
- Delete the default EFI folder which is in bootable usb
- 5.and paste the Efi to USB. Efi [here]((https://github.com/devboloji/Lenovo-Thinkpad-T450-T450s-Hackintosh-Guide-Opencore/releases)
- ### Note: IF YOU ARE USING THE CATALINA, THEN YOU NEED TO EDIT ONE THING IN CONFIG ->> open `config.plist`->`Misc`->`Security`-> `SecureBootModel`->TYPE `Disabled`.

 - 6.Restart your laptop and hit `F12`
 - 7.Select your flash drive as temporary boot option
 - 8.Now in the OpenCore menu select the name of your USB partiton
 - install.Enjoy!!!!
 ## Note: 
## 1. If you are installing Catalina it is important that you disable Airportitlwm.kext in Kernel/Add/20 of Config.plist and enable itlwm.kext instead. Read Post Install #4.
## 2. For those having a black screen or frozen installer when booting the install USB, create the USB using macOS and not Linux or Windows. Details on that [here](https://github.com/racka98/Lenovo-Thinkpad-T450-T450s-Hackintosh-Guide-Opencore/issues/2#issuecomment-732408469)

# Post Install
Once you have verifed that your machine boots properly without any issues as described in the "What Works section", proceed to do the following

### 1. Enable Verbose mode (the black screen with logs on boot up)A real hackintosh Users uses this.
In Config.plist, navigate to NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> boot-args and give a single space and add the `-v` argument

### 2. Disable ShowPicker
In the Config.plist, You can disable the boot picker screen so that you boot straight to th Apple logo by setting under `Misc` -> `Boot` -> `ShowPicker` False (NO)
Note: you can still see the boot picker with ShowPicker set to no/false by spamming Esc before the apple logo is displayed during boot.

### 3. Enable Caps lock indicator and additional Thinkpad features you used to get on Windows
  Using [YogaSMC](https://github.com/zhen-zen/YogaSMC) you can gain this functionality back. Install the YogaSMC App-Release from [here](https://github.com/zhen-zen/YogaSMC/releases).
  Install it then open it to set it up.
  
 ### 5. Boot faster
You can Disable IntelBluetoothFirmware.kext & IntelBluetoothInjector.kext to be able to Boot faster those kexts in config.plist
This is not done by default to bluetooth working.
***For those on macOS Monterey do not enable these kexts because the system will not boot***
  
### 6. Add Device Properties for Serial number, MLB, ROM, Sytem-UUID and optionally SystemProductName.
Follow this [Opencore guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#generate-a-new-serial) to set up serial number and the accompanying info to get iServices

If you want to get wired sidecar working, in Config.plist change the string in Platforminfo > Generic> SystemProductName to `MacBook9,1` (note: this causes the battery to drain faster)

### 8. Fixing static noise
When you connect headphones/earbuds via the headphone jack you will hear static noise. To fix this install alc_fix_new located in Utilities folder of this Relese Efi folder.(This may not work 100%)
Tip: To fix it, plug the headphones and close the lid and open. This may fix the static noise.
This issue may fix later on Relases.
