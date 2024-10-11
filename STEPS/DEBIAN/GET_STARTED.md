# Yequox Handbook on Drive (Debian): Get Started
Get started on building your very own Ubuntu-based Linux distribution.
## First, prepare the environment.
Set some variables to identify our work, ISO files and more:
```
export WORK=~/work
export CD=~/cd
export FORMAT=squashfs
export FS_DIR=live
```
Create the "ISO files" directory and the work:
```
sudo mkdir -p ${CD}/{${FS_DIR},boot/grub} ${WORK}/rootfs
```
### Install some packages. (optional)
We need to update the package lists:
```
sudo apt-get update
```
Install them:
```
sudo apt-get install xorriso squashfs-tools mtools qemu
```
QEMU is optional. It is only needed for testing the ISO to see how it is.
## Second, copy your system to the work.
We need the root filesystem. To copy it, choose your display manager. For example: LightDM, SDDM or GDM.
### LightDM
LightDM is a free and open-source X display manager that aims to be lightweight, fast, extensible and multi-desktop. It is used by distributions like Linux Mint. Also used by XFCE distributions, MATE distributions and Cinnamon distributions.

For LightDM users:
```
sudo rsync -av --one-file-system --exclude=/proc/* --exclude=/dev/* \
--exclude=/sys/* --exclude=/tmp/* --exclude=/home/* --exclude=/lost+found \
--exclude=/var/tmp/* --exclude=/boot/grub/* --exclude=/root/* \
--exclude=/var/mail/* --exclude=/var/spool/* --exclude=/media/* \
--exclude=/etc/fstab --exclude=/etc/mtab --exclude=/etc/hosts \
--exclude=/etc/timezone --exclude=/etc/shadow* --exclude=/etc/gshadow* \
--exclude=/etc/X11/xorg.conf* \
--exclude=/etc/lightdm/lightdm.conf --exclude=${WORK}/rootfs / ${WORK}/rootfs
```
### SDDM
SDDM (Simple Desktop Display Manager) is a display manager for the X11 and Wayland windowing systems. It is used by KDE Plasma distributions.

For SDDM users:
```
sudo rsync -av --one-file-system --exclude=/proc/* --exclude=/dev/* \
--exclude=/sys/* --exclude=/tmp/* --exclude=/home/* --exclude=/lost+found \
--exclude=/var/tmp/* --exclude=/boot/grub/* --exclude=/root/* \
--exclude=/var/mail/* --exclude=/var/spool/* --exclude=/media/* \
--exclude=/etc/fstab --exclude=/etc/mtab --exclude=/etc/hosts \
--exclude=/etc/timezone --exclude=/etc/shadow* --exclude=/etc/gshadow* \
--exclude=/etc/X11/xorg.conf* \
--exclude=/etc/sddm.conf --exclude=${WORK}/rootfs / ${WORK}/rootfs
```
### GDM
The GNOME Display Manager (GDM) is a program that manages graphical display servers and handles graphical user logins. It is owned by the GNOME team and used for its desktop environment called GNOME.

For GDM users:
```
sudo rsync -av --one-file-system --exclude=/proc/* --exclude=/dev/* \
--exclude=/sys/* --exclude=/tmp/* --exclude=/home/* --exclude=/lost+found \
--exclude=/var/tmp/* --exclude=/boot/grub/* --exclude=/root/* \
--exclude=/var/mail/* --exclude=/var/spool/* --exclude=/media/* \
--exclude=/etc/fstab --exclude=/etc/mtab --exclude=/etc/hosts \
--exclude=/etc/timezone --exclude=/etc/shadow* --exclude=/etc/gshadow* \
--exclude=/etc/X11/xorg.conf* \
--exclude=/etc/gdm/custom.conf --exclude=${WORK}/rootfs / ${WORK}/rootfs
```
### KDM (not important)
KDE Display Manager (KDM) was a display manager (a graphical login program) developed by KDE for the windowing systems X11. It was used until they replaced it with SDDM on KDE Plasma 5. No code shown because the display manager retired.
