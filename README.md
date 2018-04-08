# s5clouds8-lsi9211-8i-IR-to-IT-EFI-bootable-usb




## Creating USB Flash drive

### Preparing the drive

- [Shell_Full.efi](https://github.com/tianocore/edk2/blob/UDK2010.SR1/EdkShellBinPkg/FullShell/X64/Shell_Full.efi) - copy to `/efi/boot/bootX64.efi`

### Disabling Secure Boot (in Asus UEFI)

### Booting the drive (in Asus UEFI)


4GB USB2 stick, formatted in linux with fdisk with a 500MB primary partition, made active (bootable); then formatted mkfs.vfat as FAT16. The EFI shell was then copied over to /efi/boot/bootX64.efi.




## Hardware Used (as a baseline)

- AMD Ryzen Threadripper 1950X
- Asus Zenith Extreme X399 (TR4) w/ Noctual NH-U14S-TR4-SP3 Cooler
- G.Skill DDR4 32GB RAM @ 3200MT/s
- Fedora 27 / 4.15.14-300.fc27.x86_64
- Samsung 850 Pro 250GB SSD


## Level1Tech's Thread

This repo is a result of [posting my findings in a thread](https://forum.level1techs.com/t/asus-uefi-friendly-efi-usb-no-luck-flashing-lsi9211-8i-hba-from-ir-to-it/126344/6) on the Level1Tech's forum.  Feel free to share your findings there.

## License