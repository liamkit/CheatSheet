# ArchLinux Installation Cheat Sheet

Cheat sheet to install ArchLinux on a VMWare Fusion VM. This guide
does the minimal to create a bootable VM.

## Booting

Boot off an ArchLinux iso image.

1. choose Linux/Other Linux 3.x kernel 64-bit

## Install

Once boot, ArchLinux is running off the iso image. This step installs a 
minimal bootable ArchLinux.

```
# parted /dev/sda
(parted) mklabel msdos
(parted) mkpart primary ext4 1 100%
(parted) set 1 boot on
(parted) quit
# mkfs.ext4 /dev/sda1
# mount /dev/sda1 /mnt
# mkdir /mnt/boot
# pacstrap -i /mnt base
# genfstab -U /mnt > /mnt/etc/fstab
# arch-chroot /mnt /bin/bash
# pacman -S grub
# grub-install --recheck /dev/sda
# grub-mkconfig -o /boot/grub/grub.cfg
```
