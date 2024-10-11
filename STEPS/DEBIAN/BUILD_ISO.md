# Yequox Handbook on Drive (Debian): Build ISO
Last step is to build the ISO (and test the ISO with QEMU).
## Build the ISO.
If you are done, build the ISO:
```
sudo grub-mkrescue -o ~/live-cd.iso ${CD}
```
> Note: You can also customize the name of your ISO. For example, we are gonna use `yequoxhod-24.04-desktop-amd64.iso`.
### Test it. (optional, only needed before burning it)
Make sure you have QEMU.

To test the ISO, run:
```
qemu-system-x86_64 -cdrom ~/live-cd.iso -boot d
```
And, there you are! You are now done.
