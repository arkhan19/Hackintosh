# Audio

This guide will show you how to fix audio

## Requirement

- Install [AppleALC.kext](https://github.com/vit9696/AppleALC/releases), [Lilu.kext](https://github.com/vit9696/Lilu/releases) into /EFI/Clover/kexts/Other
- Your audio codec must be supported on [this list](https://github.com/vit9696/AppleALC/wiki/Supported-codecs) (audio codec can be found in your motherboard website)

## Remove old audio patch

If this is the first time you try to patch audio then skip this step. If you was try to patch audio with other way, please follow this to remove old audio patch.

Here's some kext you need to remove:

- realtekALC.kext
- CloverALC.kext
- VoodooHDA.kext
- HDA Blocker.kext
- HDAEnabler*.kext

Use Finder, search for:

- /Library/Extensions/
- /System/Library/Extensions/
- /Volumes/EFI/EFI/CLOVER/kexts/10.xx
- /Volumes/EFI/EFI/CLOVER/kexts/Other

Now open your config.plist file in /EFI/Clover/, remove this patch on `KernelAndKextPatches -> KextsToPatch` if you have it

- 10.11-AppleHDA/Realtek ALC...
- 10.9-10.11-AppleHDA/Realtek ALC1150
- AppleHDA/Resources/xml&gt;zml

Reboot!

## Find your audio layout

Now open this [list](https://github.com/vit9696/AppleALC/wiki/Supported-codecs), you can see your layout. Add it to your `config.plist - Devices - Audio - Inject`

For example: My audio codec is `ALC887`, my layout is `layout 1, 2, 3, 5, 7, 11, 13, 17, 18, 33, 99`, I'll try 1 or 2 or.... until I can find the perfect one

Reboot each time you try.

----------------------------------------------------------------

Thanks CorpNewt for how to remove old audio patch based on his guide!