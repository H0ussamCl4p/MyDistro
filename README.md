# MyDistro

**MyDistro** is a minimal Linux distribution created as a learning project by Choubik Houssam.  
It includes:

- Linux kernel
- BusyBox (statically linked)
- Minimal root filesystem
- Custom init script with a welcome message and ASCII art

---

## Features

- Bootable in QEMU or VirtualBox
- Minimal root filesystem with essential directories:

/bin /sbin /usr/bin /usr/sbin /etc /proc /sys /dev

- `/init` script mounts `/proc` and `/sys` and launches a shell
- Custom welcome message with ASCII art
- Optional BusyBox utilities

---

## Requirements

- Linux host (WSL or native)
- QEMU
- GNU Make
- gcc
- BusyBox source
- Linux kernel source

---

## Directory Structure

MyDistro/
├── build/ # Compiled kernel, initramfs, ISO
├── busybox/ # BusyBox source
├── linux/ # Linux kernel source
├── rootfs/ # Root filesystem
├── iso/ # ISO build directory
├── build.sh # Build script
└── README.md


---

## How to Build

Run the build script:

```bash
chmod +x build.sh
./build.sh
```

This will:

Compile the kernel and BusyBox

Build the root filesystem

Package the initramfs

Create a bootable ISO in build/MyDistro.iso

## How to Boot

### QEMU (ISO)

```bash
qemu-system-x86_64 -cdrom build/MyDistro.iso -m 512M
```
### QEMU (direct kernel + initramfs)

```bash
qemu-system-x86_64 -kernel build/bzImage -initrd build/initramfs.cpio.gz -nographic -append "console=ttyS0"
```
## Notes :

- Minimal shell; job control is limited.

- Only essential device nodes exist (/dev/console, /dev/null, /dev/zero, /dev/tty0, /dev/ttyS0, /dev/urandom).

- You can add more BusyBox utilities by editing .config in the busybox/ folder.


