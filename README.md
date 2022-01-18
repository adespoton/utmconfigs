# utmconfigs
Config files for booting Mac OS on UTM emulator for macOS (possibly for iPadOS as well).

To use these files, you'll need an installed copy of UTM.app for macOS from https://mac.getutm.app (or iOS) or from https://github.com/utmapp/UTM/releases for unstable releases, and you'll need to provide your own installation media; a basic unformatted qcow2 disk image is provided as the install target.  I've tested the configs with UTM 2 and UTM 3, on macOS and they work with both.  The following instructions assume you're installing on macOS, and will need to be tweaked slightly for iPadOS/iOS.

- Copy the .utm file you want to use into /Users/<youruser>/Library/Containers/com.utmapp.UTM/Data/Documents/ .
- For macOS 10.13 to 12, you can use https://raw.githubusercontent.com/kholia/OSX-KVM/master/fetch-macOS-v2.py (run from Terminal.app using python fetch-macOS-v2.py) to download a base install image.
- Inside the UTM interface, select your virtual machine, Select the CD/DVD drop-down, click Browse, and open the img file you downloaded with fetch-macOS-v2.py (or some other way).
- Start the virtual machine.  You may need to enter Disk Utility and format the included drive image prior to running your installation if a drive target is not available in the install window.  Disk Utility is available in a menu item in the installer.

Note: for installing OS X 10.6.8 and up, the certificate is checked to see if it has expired.  If your system clock is past the expiry date, the installer will say it can't install on the device.  To fix this, open up Terminal from the Utilities menu and type date -u 0101010115 (the last two digits is the year) or adjust the last digits to the year the installer was released, or any year between that and the year the certificate expired.  Then quit Terminal and continue your install session.  The date will automatically reset once the install is complete.

Note2: On an M1 MBP, I've had issues with keyboard input for all emulated hardware types.  I've had to add "-usbdevice keyboard" to the QEMU list.  Others have had issues with mouse detection, so I've also added "-usbdevice tablet" to the QEMU list.

System Architecture: m68k - not in UTM yet.

System: Macintosh Quadra 800 (q800)

OS: 

- System 7.5 - 8.1 / A/UX 3.x: currently waiting on upstream patches in qemu-system-m68k.  Custom builds of qemu-system-m68k are available.

System Architecture: PowerPC 

System: Mac99 based PowerMAC (mac99) - currently in UTM via qemu-system-ppc-screamer.  Note that this breaks snapshotting (pause button) for PowerPC UTM targets, which is why QEMU doesn't include screamer (audio) support in the official build.

OS: - all these currently run in qemu-system-ppc-screamer; I need to convert them to UTM configs
- Mac OS 9.0.4 - under UTM, only booting to flashing ?.  Works fine under qemu-system-ppc-screamer.
- Mac OS 9.1
- Mac OS 9.2
- Mac OS 9.2.1 - booting with -usbdevice keyboard -usbdevice tablet
- Mac OS 9.2.2
- Mac OS X Server 1.2v3
- Mac OS X Public Beta - Date needs to be set by adding -rtc base="2000-10-01",clock=vm to the QEMU arguments.
- Mac OS X 10.0
- Mac OS X Server 10.0
- Mac OS X 10.1
- Mac OS X Server 10.1
- Mac OS X 10.2
- Mac OS X Server 10.2
- Mac OS X 10.3 - Fully functional in UTM.
- Mac OS X Server 10.3  - Fully functional in UTM.
- Mac OS X 10.4
- Mac OS X Server 10.4
- Mac OS X 10.5
- Mac OS X Server 10.5

System Architecture: i386 (x86)

System: Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-6.1) (q35) - All OSes below currently not booting past the initial boot stage in UTM.
- Advanced: CPU: Penryn
- Drives: OVMF-32.bin, Type: ROM; EFI-i386.img, Type: Disk Image, Interface: USB
- Mac OS X 10.4
- Mac OS X Server 10.4
- Mac OS X 10.5
- Mac OS X Server 10.5
- Mac OS X 10.6
- Mac OS X Server 10.6

System Architecture: x86_64

System: Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-6.1) (q35)
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

System Architecture: x86_64
System: Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-6.1) (q35)
- macOS 10.14 - booting with -usbdevice keyboard, network: Emulated VLAN, vmxnet3
- macOS 10.15 - booting with -usbdevice keyboard, network: Emulated VLAN, vmxnet3

- macOS 11 - panicking or getting to (/) during boot.
- macOS 12 - not booting
  
System Architecture: aarch64
System: Apple Virtualizer
- macOS 11 - not booting
- macOS 12 - will download IPSW install image and boot using UTM 3.  No config file provided as UTM automates the entire process already.

