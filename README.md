# utmconfigs
Config files for booting Mac OS on UTM emulator for macOS (possibly for iOS as well)

Note: for installing OS X 10.6.8 and up, the certificate is checked to see if it has expired.  If your system clock is past the expiry date, the installer will say it can't install on the device.  To fix this, open up Terminal from the Utilities menu and type date -u 0101010115 (the last two digits is the year) or adjust the last digits to the year the installer was released, or any year between that and the year the certificate expired.  Then quit Terminal and continue your install session.

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
- Mac OS 9.2.1
- Mac OS 9.2.2
- Mac OS X Server 1.2v3
- Mac OS X Public Beta
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
- Drives: OVMF.bin type Disk Image interface USB, EFI-i386.img type Disk Image interface USB
- Mac OS X 10.4
- Mac OS X Server 10.4
- Mac OS X 10.5
- Mac OS X Server 10.5
- Mac OS X 10.6
- Mac OS X Server 10.6

System Architecture: x86_64

System: Standard PC (Q35 + ICH9, 2009) (alias of pc-q35-6.1) (q35)
- Advanced: CPU: Penryn with CPU flags sse4.1, sse4.2, ssse3
- Mac OS X 10.6
- Mac OS X Server 10.6
- Mac OS X 10.7 - booting with -usbdevice keyboard and Network e1000
- OS X 10.8 - booting with -usbdevice keyboard and Network e1000
- OS X 10.9 - booting with -usbdevice keyboard and Network usb-net
- OS X 10.10 - booting with -usbdevice keyboard, no network
- OS X 10.11
- macOS 10.12
- macOS 10.13
- macOS 10.14
- macOS 10.15
- macOS 11
- macOS 12
