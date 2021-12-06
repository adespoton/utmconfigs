# utmconfigs
Config files for booting Mac OS on UTM emulator for macOS (possibly for iOS as well)

Note: for installing OS X 10.6.8 and up, the certificate is checked to see if it has expired.  If your system clock is past the expiry date, the installer will say it can't install on the device.  To fix this, open up Terminal from the Utilities menu and type date -u 0101010115 (the last two digits is the year) or adjust the last digits to the year the installer was released, or any year between that and the year the certificate expired.  Then quit Terminal and continue your install session.  The date will automatically reset once the install is complete.

Note2: On an M1, I've had issues with keyboard input for all emulated hardware types.  I've had to add "-usbdevice keyboard" to the QEMU list.

System Architecture: m68k

System: Macintosh Quadra 800 (q800)

OS: 

- System 7.5 - 8.1 / A/UX 3.x: currently waiting on upstream patches in qemu-system-m68k.  Custom builds of qemu-system-m68k are available.

System Architecture: PowerPC

System: Mac99 based PowerMAC (mac99)

OS: - all these currently run in qemu-system-ppc-screamer; I need to convert them to UTM configs
- Mac OS 9.0.4
- Mac OS 9.1
- Mac OS 9.2
- Mac OS 9.2.1 - booting with -usbdevice keyboard
- Mac OS 9.2.2
- Mac OS X Server 1.2v3
- Mac OS X Public Beta - Date needs to be set with -rtc base="2000-10-01",clock=vm
- Mac OS X 10.0
- Mac OS X Server 10.0
- Mac OS X 10.1
- Mac OS X Server 10.1
- Mac OS X 10.2
- Mac OS X Server 10.2
- Mac OS X 10.3 - currently broken in qemu-system-ppc-screamer; this will be my first UTM migration attempt.
- Mac OS X Server 10.3
- Mac OS X 10.4
- Mac OS X Server 10.4
- Mac OS X 10.5
- Mac OS X Server 10.5

System Architecture: i386 (x86)

System: Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-6.1) (q35)
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
- Mac OS X 10.6
- Mac OS X Server 10.6
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
- macOS 10.15

- macOS 11
- macOS 12
