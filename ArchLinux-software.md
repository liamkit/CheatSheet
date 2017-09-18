# ArchLinux Software Installation

Install some useful software over base Archlinux.


```
# pacman -S sudo
# pacman -S openntpd
# pacman -S openssh
# systemctl enable sshd.service

# pacman -S xorg-server
# pacman -S xorg-xinit
# pacman -S xf86-video-vmware
# pacman -S xterm
# echo "xterm" > ~/.xinitrc; chmod +x ~/.xinitrc
# startx -- -retro

# pacman -S lxde
# pacman -S polkit
# echo "exec startlxde" > ~/.xinitrc
# startx -- -retro
```
