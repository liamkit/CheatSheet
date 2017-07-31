# ArchLinux Installation Cheat Sheet

Cheat sheet to install ArchLinux on a VMWare Fusion VM using
EFI. Compare to normal installation, The only different is in
grub-install. This guide does the minimal to create a bootable VM.


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
# genfstab -U /mnt >> /mnt/etc/fstab
# arch-chroot /mnt /bin/bash

# pacman -S grub efibootmgr
# grub-install --efi-directory=/boot --recheck /dev/sda
# grub-mkconfig -o /boot/grub/grub.cfg
# exit
# reboot
```



## Basic
The following is not required for booting but something you probably would want to do after first boot:

# pacman -S openssh net-tools sudo
# echo {hostname} > /etc/hostname
# cd /etc/netctl; sed -e "s@eth0@{etherinterface}@" examples/ethernet-dhcp > {etherinterface}
# netctl enable {etherinterface}
# netctl start {etherinterface}
# systemctl enable sshd.service
# useradd {somebody}
# passwd {somebody}
# mkdir /home/{somebody}; chown {somebody}:{somebody} /home/{somebody}
