# Yequox Handbook on Drive (Ubuntu): Preparing the CD directory tree
Third step is to prepare the CD directory tree.
## Fourth, copy the kernel and other important files included in the chroot.
To copy the kernel and other important files included in the chroot, run:
```
export kversion=`cd ${WORK}/rootfs/boot && ls -1 vmlinuz-* | tail -1 | sed 's@vmlinuz-@@'`
sudo cp -vp ${WORK}/rootfs/boot/vmlinuz-${kversion} ${CD}/${FS_DIR}/vmlinuz
sudo cp -vp ${WORK}/rootfs/boot/initrd.img-${kversion} ${CD}/${FS_DIR}/initrd.img
```
## Copy EFI (only for UEFI)
Copy EFI:
```
sudo cp ${WORK}/rootfs/boot/efi ${CD}/ -R
```
If it's on uppercase, run this instead:
```
sudo cp ${WORK}/rootfs/boot/EFI ${CD}/ -R
```
## Convert the directory tree to a SquashFS (required)
Unmount bind mounted directories:
```
sudo umount ${WORK}/rootfs/proc
sudo umount ${WORK}/rootfs/sys
sudo umount ${WORK}/rootfs/dev
```
Convert it:
```
sudo mksquashfs ${WORK}/rootfs ${CD}/${FS_DIR}/filesystem.${FORMAT} -noappend
```
## Make some (important) files
Calculate MD5 & make the file:
```
find ${CD} -type f -print0 | xargs -0 md5sum | sed "s@${CD}@.@" | grep -v md5sum.txt | sudo tee -a ${CD}/md5sum.txt
```
Create & edit the grub configuration:
```
sudo nano ${CD}/boot/grub/grub.cfg
```
Add:
```
set default="0"
set timeout=10

menuentry "Live system" {
linux /casper/vmlinuz boot=casper quiet splash
initrd /casper/initrd.img
}

menuentry "Live system in safe mode" {
linux /casper/vmlinuz boot=casper xforcevesa quiet splash
initrd /casper/initrd.img
}

menuentry "Live system CLI mode" {
linux /casper/vmlinuz boot=casper textonly quiet splash
initrd /casper/initrd.img
}

menuentry "Live system persistent mode" {
linux /casper/vmlinuz boot=casper persistent quiet splash
initrd /casper/initrd.img
}

menuentry "Live system from RAM" {
linux /casper/vmlinuz boot=casper toram quiet splash
initrd /casper/initrd.img
}

menuentry "Check Disk for Defects" {
linux /casper/vmlinuz boot=casper integrity-check quiet splash
initrd /casper/initrd.img
}

menuentry "Memory Test" {
linux16 /boot/memtest86+.bin
}

menuentry "Boot from the first hard disk" {
set root=(hd0)
chainloader +1
}
```
Save it and you're done! Next is to build the ISO to enjoy your distribution.
