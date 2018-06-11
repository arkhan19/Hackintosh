# macOS installtion

## BIOS/UEFI:

To prepare your PC to install macOS, you need to set your BIOS/UEFI follow those option. Upgrade BIOS to latest version if you can.


```
Virtualization : Enabled
VT-d : Disabled
XHCI Hand-Off : Enabled
Legacy USB Support: Auto/Enabled
IO SerialPort : Disabled
Network Stack : Disabled
XMP Profile :  Auto / Profile 1/Enabled
UEFI Booting set to Enabled and set Priority over Legacy
Secure Boot : Disabled
Fast Boot : Disabled
OS Type: Other OS
Wake on LAN : Disabled
```
AMD/NVIDIA GPU:

```
Integrated Graphics : Disabled 
Graphics: PEG/PCIe Slot 1
Initial Display Output : PCIe 1 Slot
``` 

Intel iGPU:

```
Integrated Graphics : Enabled
Graphics: IGD/Integrated/iGPU/CPU Graphics
DVMT Pre-Allocated : 64MB or higher
```

Now your PC is ready to install, booting into Clover and select macOS install. You may need to wait 5-10 minutes till setup screen.

After install, you need to re-install Clover package like you did before you install macOS to your hard drive and copy kext, config.plist to your EFI partition of your hard drive to boot without bootable drive.


