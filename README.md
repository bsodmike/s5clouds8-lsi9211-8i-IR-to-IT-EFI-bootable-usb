# s5clouds8-lsi9211-8i-IR-to-IT-EFI-bootable-usb

## Creating USB Flash drive

The following 'spec' has been confirmed to work

- Sony 4GB USB2.0 Flash Drive.  I have been _told_ that USB3 sticks may not work.

Format as follows, use `lsblk -f` and `fdisk -l` to locate the correct device and replace `/dev/sdX` below

- Wipe the drive with `dd if=/dev/null of=/dev/sdX bs=16k status=progress`
- `fdisk /dev/sdX`
  - Select `o` to create new empty DOS partition table.
  - `n` and choose to create a primary partition, where the last sector is `+500M`.
  - `w` to write and exit
- `fdisk /dev/sdX1` + `a` to set the primary partition as bootable (active). Choose `w` to write and exit.
- `sudo mkfs.vfat /dev/sdX1` to format as FAT16.

### Preparing the drive

Mount and copy the contents of the `usb` folder to the root of the USB drive.  Here's a breakdown of where these files have been obtained from 

- `/efi/boot/bootX64.efi` - This is [Shell_Full.efi](https://github.com/tianocore/edk2/blob/UDK2010.SR1/EdkShellBinPkg/FullShell/X64/Shell_Full.efi) from the Tianocore Github repo; the X64 full-shell from the `UDK2010.SR1` branch.  It's _the oldest_ and I needed to find a version old enough that would work with `sas2flash.efi`.  Refer [details by `boris_d` and the dreaded _"InitShellApp: Application not started from Shell"_ error when using a newer version of the Tianocore shell.](https://forums.freenas.org/index.php?threads/how-to-flash-lsi-9211-8i-using-efi-shell.50902/)

- `sas2flash.efi`: from `9211-8i_Package_P20_IR_IT_Firmware_BIOS_for_MSDOS_Windows.zip` 
- `2118it.bin`: from `Installer_P20_for_UEFI.zip` ([link](https://docs.broadcom.com/docs/12350820))
- `mptsas2.rom`: from `Installer_P20_for_UEFI.zip` ([link](https://docs.broadcom.com/docs/12350530))

The zip files mentioned above are included in the root of this repo for archival purposes.

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

Much thanks to [Whizdumb](https://forum.level1techs.com/u/Whizdumb) for pointing me in the right direction with crucial info about using USB2 drives.

### References

- https://forums.freenas.org/index.php?threads/how-to-flash-lsi-9211-8i-using-efi-shell.50902/
- https://forums.servethehome.com/index.php?threads/tutorial-updating-ibm-m1015-lsi-9211-8i-firmware-on-uefi-systems.11462/

## License

This project is licensed under the terms of the MIT License.