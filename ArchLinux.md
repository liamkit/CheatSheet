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
# exit
# reboot
```

## Network
Network is essential these days. You'll need the name of your ethernet interface, e.g. eth0.
Use ip addr to find the name.  To install dhcp client:

```
# echo {hostname} > /etc/hostname
# hostname {hostname}
# cd /etc/netctl
# sed -e "s@{eth0}@ens33@" examples/ethernet-dhcp > ethernet-dhcp
# netctl enable ethernet-dhcp
# netctl start ethernet-dhcp

# pacman -S openssh
# systemctl enable sshd
```



## Useful Commands

+ pacman -Q - query package database
