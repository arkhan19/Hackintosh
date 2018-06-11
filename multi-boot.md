# Multi-boot

I didn't use MBR/Legacy for 7 years so my guide only support for GPT/UEFI user, sorry if you using old machine!

## Windows -> macOS

So you want to install macOS without re-install Windows, here's how to do it:

- Expend your EFI partition to 200MB by partition tool (you can use Active@ Partition Manager on Windows or GParted Live Boot/Ubuntu as well)
- Create a new partition for macOS (format to FAT32 or NTFS or exFAT), do not leave it as free space.

Now you are ready to install macOS, boot in and format macOS partition to HFS/APFS and install!

## macOS -> Windows

To install Windows you need a bootable Windows installer, if you don't have it you can use Boot Camp to create too. 

If you using Boot Camp then don't create Windows partition with Boot Camp, we just need to create a bootable installer. Turn off internet before create to prevent macOS download Boot Camp software to your drive.

Now open Disk Utility, click to View -> Show all drive. Click to your disk -> Partition, resize your Windows partition and format it to HFS+J (do not format it to FAT32/exFAT because it'll create MBR partition)

After that boot into Windows installer, delete that Windows partition you just format to HFS and install on that free space. Windows should be installing now!

## Linux

For Linux, I usually install Ubuntu. With Linux you can install it like normal, no matter what file-system you format to. You can format it to ext4 later on Ubuntu later and install. Clover can dectect new entry and add it into Bootloader.

## Clover EFI

In case after you installed Windows/Linux and Clover goes, you need to use BIOS/UEFI settings to set it back. If you can't boot after you set it back then you need to use [EasyUEFI](https://www.easyuefi.com/index-us.html) on Windows or [rEFInd](https://sourceforge.net/projects/refind/files/0.11.2/) on Linux or Live Boot to delete old Clover EFI boot option and add a new boot option to `/EFI/Clover/CLOVERX64.efi`