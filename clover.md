# Clover Bootloader

After create a bootable macOS installer, it's time to install Clover Bootloader.

Download latest version [here](https://github.com/Dids/clover-builder/releases/) (thank to Dids for his automatically project)

Open the package (.pkg), change install location to your bootable drive. Open customise, select to:

- Setup Clover Bootloader to install for UEFI or BIOS
- Drivers64UEFI -> apfs_patched, AptioMemoryFix

Now mount your EFI partition with [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) and setup config.plist

## config.plist

You need to setup config.plist based on your hardware. 

You can use [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) to edit it in /EFI/Clover/config.plist

### Acpi

#### Patches

- This is where you can add your own patch to rename ACPI device, which for some case can fix audio, Intel ME engine, iGPU,....
- If you want to install macOS for the first time, you won't need any ACPI patch.

#### SSDT

- If you are using Haswell CPU or higher, turn on PluginType in Generate box.

### Boot

- For the first time boot, you need to turn on verbose (-v), debug=0x100 in case you are getting kernel panic
- Default Boot Volume: You can set Clover to boot into which volume everytime you boot up
- Timeout: Timeout for boot option

### Devices

- USB: Turn on Inject, Add ClockID, FixOwnership

### Gui

- Scan: Auto=Yes
- Language: select your language
- Screen Resolution: select your screen resolution

### Graphics

- If you using Intel HD without dGPU, select Inject Intel
- If you using NVIDIA GPU from 710 or lower generation, select Inject NVIDIA

### Kernel and Kext Patches

- Add this USB port limit patch for High Sierra

```
Comment: Change 15 port limit to 24 in XHCI kext 10.13 PB1
Find: 837D8C10
Name: AppleUSBXHCIPCI
Replace: 837D8C1B
```
- For Sierra

```
Comment change 15 port limit to 20 in XHCI kext (9-series) 10.12
Find 83BD74FF FFFF10
Name AppleUSBXHCIPCI
Replace 83BD74FF FFFF15

Comment change 15 port limit to 26 in XHCI kext (100-series) 10.12
Find 83BD74FF FFFF10
Name AppleUSBXHCIPCI
Replace 83BD74FF FFFF1B
```

### Rt Variables

- ROM: UseMacAddr0
- BooterConfig: 0x28
- CsrActiveConfig: 0x67

### SMBIOS

You need to select SMBIOS based on your CPU generation, there's an button at left corner to select and generate Series Number, Board Series Number for each SMBIOS

- Sandy Bridge: iMac12,1 & iMac12,2
- Ivy Bridge: iMac13,1 & iMac13,2
- Haswell: iMac14,1 & iMac14,2 & iMac14,4 & iMac15,1
- Broadwell: iMac16,1 & iMac16,2 
- Skylake: iMac17,1
- Kaby Lake/Coffee Lake: iMac18,1 & iMac18,2 & iMac18,3
- Skylake-W: iMacPro1,1

### System Parameters

- Inject Kexts: Yes
- Inject System ID: Yes
- If you using NVIDIA GPU from 750 or newer then enable NvidiaWeb

## Kexts

To install kext, download your kext and grab it to /EFI/Clover/kexts/Other

For the first time booting you only need 2 kexts:

- [FakeSMC.kext](https://bitbucket.org/RehabMan/os-x-fakesmc-kozlek/downloads/)
- [USBInjectAll.kext](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/)

If you using iGPU then you need this kext too:

- [IntelGraphicsFixup.kext](https://github.com/lvs1974/IntelGraphicsFixup/releases)
- [Lilu.kext](https://github.com/vit9696/Lilu/releases)

If you using AMD GPU then you need this kext too:

- [WhateverGreen.kext](https://github.com/vit9696/WhateverGreen/releases)
- [Lilu.kext](https://github.com/vit9696/Lilu/releases)

If you using 200-series motherboard then you need this kext too:

- [XHCI-200-series-injector.kext](Kext/XHCI-200-series-injector.kext.zip)

If you using 300-series motherboard then you need this kext too:

- [XHCI-300-series-injector.kext](Kext/XHCI-300-series-injector.kext.zip)

If you using x99 motherboard then you need this kext too:

- [XHCI-x99-injector.kext](XHCI-x99-injector.kext.zip)

## drivers64UEFI

- [apfs.efi](https://github.com/piiiggg/apfs.efi): To booting into APFS partition, you need this efi file to boot into macOS after install.
- apfs_patched.efi: Same like apfs.efi but modify to kill debug log
- AptioMemoryFix.efi: This will fix UEFI APTIO Firmware issues to make your system booting into macOS
- OsxAptioFix2/3Drv-64.efi: Same as AptioMemoryFix but it doesn't support native NVRAM and little bad than AptioMemoryFix, use this when AptioMemoryFix.efi broken
- EmuVariableUefi-64.efi: This will emulate NVRAM to make it working on macOS when your NVRAM not working/don't have. Some PC/Laptop even using AptioMemoryFix.efi but still not have native NVRAM. Use this if you need, also 

Now you are ready to [install macOS](install.md)

