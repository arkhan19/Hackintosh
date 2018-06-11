# Graphics

## Intel

Notes:

```
HD2000/HD2500, not supported
HD4600/HD4400/Mobile - no native support
```

For Intel iGPU:

- Enable `Inject Intel` in: `config.plist - Graphics - Inject Intel`
- Install [IntelGraphicsFixup.kext](https://github.com/lvs1974/IntelGraphicsFixup/releases) & [Lilu.kext](https://github.com/vit9696/Lilu/releases) & [Shiki.kext](https://github.com/vit9696/Shiki/releases)
- Enable iGPU/Intel HD in BIOS/UEFI
- Allow 64MBs or higher for DVMT-shared memory (some BIOS doesn't allow you to change it, please install [this kext](https://github.com/BarbaraPalvin/IntelGraphicsDVMTFixup/releases) to bypass
- [Enable power management for your CPU](pm.md)

For HD4600/HD4400/Mobile, follow [this](https://www.tonymacx86.com/threads/fix-hd4200-hd4400-hd4600-hd5600-on-10-11.175797/)

## NVIDIA

### Legacy NVIDIA GPU

Old NVIDIA GPU like 6/5/4/..., you don't need to install NVIDIA Web Driver. macOS already support it.

Some case you need to enable `Inject NVIDIA` in `config.plist - Graphics - Inject NVIDIA` if your GPU not working properly

You still need those kext for ACPI patching:

- Install [NvidiaGraphicsFixup.kext](https://github.com/lvs1974/NvidiaGraphicsFixup/releases) & [Lilu.kext](https://github.com/vit9696/Lilu/releases) & [Shiki.kext](https://github.com/vit9696/Shiki/releases)

### Modern NVIDIA GPU

If you using NVIDIA GPU like 7/9/10-series then you will need to install NVIDIA Web Driver

Follow those step to install NVIDIA Web Driver

- Make sure NVRAM working, if you are using `AptioMemoryFix.efi` from latest Clover package then NVRAM is working
- Install [NvidiaGraphicsFixup.kext](https://github.com/lvs1974/NvidiaGraphicsFixup/releases) & [Lilu.kext](https://github.com/vit9696/Lilu/releases) & [Shiki.kext](https://github.com/vit9696/Shiki/releases)
- Search the right NVIDIA Web Driver for your macOS build number at [here](https://www.tonymacx86.com/nvidia-drivers/)
- Install and reboot!

## AMD

Here's [Radeon Compatibility Guide](https://www.tonymacx86.com/threads/radeon-compatibility-guide-ati-amd-graphics-cards.171291/) from tonymacx86

Remember if your GPU needs `RadeonDeInit` or not

- Install [WhateverGreen.kext](https://github.com/vit9696/WhateverGreen/releases) & [Lilu.kext](https://github.com/vit9696/Lilu/releases) & [Shiki.kext](https://github.com/vit9696/Shiki/releases)
- If your GPU needs `RadeonDeInit` enable it in `config.plist - Graphics - RadeonDeInit`

# HDMI Audio

## Intel

If your Intel HD working properly then HDMI audio will working

Notes:

```
HD540: Supports 1x display, boot fails with 2x display; 2nd display hot plug works
```

## NVIDIA

If your NVIDIA GPU working properly then HDMI audio will working

Notes:

```
10xx:
No HDMI audio on HDMI port after boot, fixes:
DP-HDMI adapter
DVI-HDMI adapter
Hot plug HDMI display after Desktop appears
```

```
GTS 450, GTX 550/550ti, GTX 560/560ti; no native support
450: no known fix

550/550ti: Patch AppleHDA binary
Find: 14 00 de 10
Replace: 15 00 de 10

560/560ti/Quadro 4000: Patch AppleHDAController binary
Find: de 10 ea 0b
Replace: de 10 e5 0b
```

## AMD

If your AMD GPU working properly then HDMI audio will working

Notes:

```
Vega:
10.13: HDMI audio working
10.12: HDMI audio not working

Polaris:
10.13: HDMI/DP audio working
10.12: HDMI/DP audio not working
```

# Dual-GPU

You need to enable Intel HD working together with AMD/NVIDIA for encoding/decoding faster and prevent crashing on Final Cut Pro X

- Follow iGPU guide to enable Intel HD, but set iGPU Multi-monitor to `on` and set primary display to `PEG/PCIe` in BIOS/UEFI settings
- For Kaby Lake, use `0x59120003` in `config.plist  - Graphics - ig-platform-id` to prevent crashing when boot

------------------------

Thank toleda from tonymacx86 for all of HDMI audio information!