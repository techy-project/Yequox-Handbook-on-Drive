# Yequox Handbook on Drive (Ubuntu): Modifying
Well, the second step is modifying.
## Third, chroot and modify.
Before chrooting, please mount them so it will fully work.
Run these before chrooting:
```
sudo mount  --bind /dev/ ${WORK}/rootfs/dev
sudo mount -t proc proc ${WORK}/rootfs/proc
sudo mount -t sysfs sysfs ${WORK}/rootfs/sys
sudo mount -o bind /run ${WORK}/rootfs/run
```
And now, chroot:
```
sudo chroot ${WORK}/rootfs /bin/bash
```
The first command we are gonna run is:
```
LANG=en_US.UTF-8
```
It will set the language. (for example, en_US.UTF-8 is the American English language.)

### Install additional software
Update the package lists again:
```
apt update
```
Install `casper`:
```
apt install casper
```
If you want a installer for your Ubuntu-based distribution, run (optional):
```
apt install ubiquity-frontend-gtk
```
If it's running KDE Plasma, run (optional):
```
apt install ubiquity-frontend-kde
```
Install any packages you want on the CD. For example:
```
apt install gparted xfsprogs dosfstools ntfsprogs
```
The packages we are using:

- GParted (gparted): GUI partitioning tool.
  - xfsprogs, dosfstools & ntfsprogs: Install these to support some formats.
 
Update initramfs:
```
update-initramfs -u
```
Clean all the extra logs:
```
apt clean
```
Create a user:
```
useradd -s /bin/bash -d /home/live/ -m -G sudo,wheel live
```
Make a password for your user (optional):
```
passwd live
```
Remove non-live user:
```
userdel nonlive
```
Replace `nonlive` with your username that is used on your system.

Clear command history and exit:
```
history -c && exit
```
