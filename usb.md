# Patch USB port

If you are using USB port limit patch before on `config.plist`, it's just a temporary solution to you install macOS properly on any USB port. When you done, you have to create your own SSDT for `USBInjectAll.kext`, it'll also disable unneeded port to save power. And help your hack can sleep better

How to create SSDT for `USBInjectAll.kext`, check [this](https://www.tonymacx86.com/threads/guide-creating-a-custom-ssdt-for-usbinjectall-kext.211311/)