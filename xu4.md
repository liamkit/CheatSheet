# Odroid XU4

## Disk Image
This doc only describes the disk image layout using a SD card. Alternatively, you can use a eMMC card,
which allows booting up much faster.  The following table shows the offsets in sector (512b) of the
different components:

|Software|Offset (512 sector)|Description|
|--------|-------------------|-----------|
|Bl1|1|(1st stage boot loader)|
|Bl2|31|(2nd stage boot loader)|
|U-Boot|63|(u-boot)|
|Tzsw|2111|(trust zone - some security stuff to enable the processor in the kernel)|

See http://lists.denx.de/pipermail/u-boot/2014-November/195408.html<br/>
See https://github.com/hardkernel/u-boot/raw/odroidxu3-v2012.07/sd_fuse/hardkernel_1mb_uboot
