# ArchLinux Installation Cheat Sheet *NOT COMPLETED*

Cheat sheet to install ArchLinux on a VMWare Fusion VM using EFI. This guide
does the minimal to create a bootable VM.


## Booting

1. choose Linux/Other Linux 3.x kernel 64-bit
2. once vm is create, edit VM configuration file, e.g. ~/Documents/Virtual Machines.localized/{vmname}.vmwarevm/{vmname}.vmx and add the line 
```
firmware = "efi"
```
3. restart the VM

## Install

Once boot, ArchLinux is running off the iso image. This step installs a 
minimal bootable ArchLinux.

```
# parted /dev/sda
(parted) mklabel gpt
(parted) mkpart ESP fat32 1MiB 513MiB
(parted) mkpart primary ext4 513MiB 100%
(parted) set 1 boot on
# mkfs.fat -F32 /dev/sda1
# mkfs.ext4 /dev/sda2

# mount /dev/sda2 /mnt
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

# pacstrap /mnt base
# genfstab -U /mnt > /mnt/etc/fstab
# arch-chroot /mnt /bin/bash

# pacman -S refind-efi
# cp /usr/share/refind/refind_x64.efi /boot/EFI/Boot/bootx64.efi
# cp -r /usr/share/refind/drivers_x64 /boot/EFI/Boot/
# exit
# reboot
```















[https://wiki.archlinux.org/index.php/User:Soloturn/Quick_Installation_guide_UEFI]

