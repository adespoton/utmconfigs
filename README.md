# utmconfigs
Config files for booting Mac OS on UTM emulator for macOS (possibly for iPadOS as well).

To use these files, you'll need an installed copy of UTM.app for macOS from https://mac.getutm.app (or iOS) or from https://github.com/utmapp/UTM/releases for unstable releases, and you'll need to provide your own installation media; a basic unformatted qcow2 disk image is provided as the install target.  I've tested the configs with UTM 2 and UTM 3, on macOS and they work with both.  The following instructions assume you're installing on macOS, and will need to be tweaked slightly for iPadOS/iOS.

- Copy the .utm file you want to use into /Users/[youruser]/Library/Containers/com.utmapp.UTM/Data/Documents/ .  This can be done by double-clicking the unzipped file.
- For macOS 10.13 to 12, you can use https://raw.githubusercontent.com/kholia/OSX-KVM/master/fetch-macOS-v2.py (run from Terminal.app using python fetch-macOS-v2.py) to download a base install image.  Other installer locations are provided inside the config notes.
- If using full installers instead of just the baseconfig.img files, you can run https://github.com/BITespresso/createinstalliso  to convert the .app installers to a bootable .iso.  Note that some of these can't be converted from an M1 Mac (but can be converted from inside an x86-64 UTM guest).
- Inside the UTM interface, select your virtual machine, Select the CD/DVD drop-down, click Browse, and open the img file you downloaded with fetch-macOS-v2.py (or some other way).
- Start the virtual machine.  You may need to enter Disk Utility and format the included drive image prior to running your installation if a drive target is not available in the install window.  Disk Utility is available in a menu item in the installer.

Note: for installing OS X 10.6.8 and up, the certificate is checked to see if it has expired.  If your system clock is past the expiry date, the installer will say it can't install on the device.  To fix this, open up Terminal from the Utilities menu and type date -u 0101010115 (the last two digits is the year) or adjust the last digits to the year the installer was released, or any year between that and the year the certificate expired.  Then quit Terminal and continue your install session.  The date will automatically reset once the install is complete.

Note2: On an M1 MBP, I've had issues with keyboard input for all emulated hardware types.  I've had to add "-usbdevice keyboard" to the QEMU list for OS X 10.2 and up.  UTM already adds a tablet device by default.

Note3: The X86 installs depend on OpenCore EFI to boot correctly.  If you want to roll your own with tweaked drivers etc, the latest version is available at https://github.com/acidanthera/OpenCorePkg/releases/

## System Architecture: m68k - bootable builds not available in UTM yet.

### System: Macintosh Quadra 800 (q800)
- currently waiting on upstream patches in qemu-system-m68k.  Custom builds of qemu-system-m68k are available.

### OS: 
- Don't work in UTM yet:
- System 7.5.0
- 8.1
- A/UX 3.x 

## System Architecture: PowerPC 

### System: Mac99 based PowerMAC (mac99) 
- currently in UTM via qemu-system-ppc-screamer.  Note that this breaks snapshotting (pause button) for PowerPC UTM targets, which is why QEMU doesn't include screamer (audio) support in the official build.

### OS: 
- all these currently run in qemu-system-ppc-screamer; I need to convert them to UTM configs
- Mac OS 9.0.4 - Requires G4 Cube Install CD (Mac OS ROM >= 5.6) and via=cuda in Machine Properties.  No keyboard support even with -usbdevice keyboard. Memory must be greater than 64MB and less than 1024MB.
- Mac OS 9.1 - booting with network and audio with -usbdevice keyboard
- Mac OS 9.2.0
- Mac OS 9.2.1 - booting with network and audio with -usbdevice keyboard
- Mac OS 9.2.2 - booting with network and audio with -usbdevice keyboard
- Mac OS X Server 1.2v3 - has issues with g3Beige emulation.  Won't boot.
- Mac OS X Public Beta - Date needs to be set by adding -rtc base="2000-10-01",clock=vm to the QEMU arguments. Requires via=cuda in Machine Properties.  First boot must be done with networking disabled, to disable the Apple time server, otherwise NTP clobbers the RTC base and PB refuses to run.
- Mac OS X 10.0 - Requires via=cuda in Machine Properties.  Capture and uncapture mouse a few times to get mouse and keyboard input.
- Mac OS X Server 10.0 - Requires via=cuda in Machine Properties.  Capture and uncapture mouse a few times to get mouse and keyboard input.
- Mac OS X 10.1 - Requires via=cuda in Machine Properties.  Capture and uncapture mouse a few times to get mouse and keyboard input. I needed to set my CPU to G3 to boot.
- Mac OS X Server 10.1 - Requires via=cuda in Machine Properties.  Capture and uncapture mouse a few times to get mouse and keyboard input.  I needed to set my CPU to G3 to boot.
- Mac OS X 10.2 - booting with network and audio with -usbdevice keyboard
- Mac OS X Server 10.2 - booting with network and audio with -usbdevice keyboard
- Mac OS X 10.3 - booting with network and audio with -usbdevice keyboard
- Mac OS X Server 10.3 - booting with network and audio with -usbdevice keyboard
- Mac OS X 10.4 - booting with network and audio with -usbdevice keyboard
- Mac OS X Server 10.4 - booting with network and audio with -usbdevice keyboard
- Mac OS X 10.5 - booting with network and audio with -usbdevice keyboard
- Mac OS X Server 10.5 - booting with network and audio with -usbdevice keyboard

## System Architecture: i386 (x86)

### System: Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-6.1) (q35) - All OSes below currently not booting past the initial boot stage in UTM.
- Advanced: CPU: Penryn
- Drives: OVMF.bin, Type: ROM; EFI-Legacy.img, Type: Disk Image, Interface: USB
  - or
- Drives: OVMF-32.bin, Type: ROM; EFI-i386.img, Type: Disk Image, Interface: USB
- Mac OS X 10.4
- Mac OS X Server 10.4
- Mac OS X 10.5
- Mac OS X Server 10.5
- Mac OS X 10.6
- Mac OS X Server 10.6

## System Architecture: x86_64 (Legacy)

### System: Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-6.1) (q35)
- Advanced: CPU: Penryn with CPU flags sse4.1, sse4.2, ssse3
- Drives: OVMF.bin, Type: ROM; EFI-LEGACY.img, Type: Disk Image, Interface: USB
- Mac OS X 10.6 - panicking or getting to (/) during boot.
- Mac OS X Server 10.6 - panicking or getting to (/) during boot.
- Mac OS X 10.7 - booting with -usbdevice keyboard, Network: Emulated VLAN, e1000
- OS X 10.8 - booting with -usbdevice keyboard, Network: Emulated VLAN, e1000
- OS X 10.9 - booting with -usbdevice keyboard, Network: Emulated VLAN, usb-net
- OS X 10.10 - booting with -usbdevice keyboard, no network
- OS X 10.11 - booting with -usbdevice keyboard, network: Emulated VLAN, vmxnet3
- macOS 10.12 - booting with -usbdevice keyboard, network: Emulated VLAN, vmxnet3
- macOS 10.13 - booting with -usbdevice keyboard, network: Emulated VLAN, vmxnet3

## System Architecture: x86_64 (Modern)

System: Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-6.1) (q35)
- Advanced: CPU: Penryn with CPU flags sse4.1, sse4.2, ssse3
- Drives: OVMF.bin, Type: ROM; EFI-LEGACY.img, Type: Disk Image, Interface: USB
- macOS 10.14 - booting with -usbdevice keyboard, network: Emulated VLAN, vmxnet3
- macOS 10.15 - booting with -usbdevice keyboard, network: Emulated VLAN, vmxnet3 - unstable, prone to drive corruption.

- macOS 11 - booting with -usbdevice keyboard, network: Emulated VLAN, vmxnet3 - unstable, prone to drive corruption.
- macOS 12 - haven't attempted yet.
  
## System Architecture: aarch64
System: Apple Virtualizer
- macOS 11 - not compatible
- macOS 12 - will download IPSW install image and boot using UTM 3+.  No config file provided as UTM automates the entire process already.  Can only use raw disk images at this time, so create one of the appropriate size (48GB or larger).  Image cannot be resized once it has been created.

