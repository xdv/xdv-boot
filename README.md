# XDV-Boot - XDV Bootloader

**Version:** 0.2.0  
**Status:** Implemented  
**Language:** Dust Programming Language (DPL)  

---

## Overview

xdv-boot is the bootloader for the XDV Operating System. It provides:

- Stage 1: MBR (512-byte bootloader)
- Stage 2: Extended boot loader
- GDT/IDT setup
- Paging enablement
- Disk I/O
- XDVFS mounting
- Kernel loading

## Directory Structure

```
xdv-boot/
├── State.toml
├── README.md
└── src/
    ├── boot_mbr.ds              # Stage 1: MBR bootloader
    ├── boot_mbr_tests.ds       # MBR tests
    ├── boot_stage1.ds          # Stage 2: Basic init
    ├── boot_stage1_tests.ds    # Stage 1 tests
    ├── boot_gdt.ds             # GDT setup
    ├── boot_gdt_tests.ds       # GDT tests
    ├── boot_idt.ds             # IDT setup
    ├── boot_idt_tests.ds       # IDT tests
    ├── boot_paging.ds          # Paging enable
    ├── boot_paging_tests.ds    # Paging tests
    ├── boot_disk.ds            # Disk I/O
    ├── boot_disk_tests.ds      # Disk tests
    ├── boot_xdvfs_mount.ds     # Mount XDVFS
    ├── boot_xdvfs_mount_tests.ds# XDVFS mount tests
    └── boot_kernel_load.ds     # Kernel loading
    └── boot_kernel_load_tests.ds# Kernel load tests
```

## Implemented Features

- MBR boot sector with magic number
- Basic boot initialization
- GDT (Global Descriptor Table) setup
- IDT (Interrupt Descriptor Table) setup
- Paging enablement
- Disk I/O operations
- XDVFS mounting
- Kernel loading

## Build

```bash
dust check xdv-boot/src
```

## Status

- [x] MBR bootloader
- [x] Stage 1 init
- [x] GDT setup
- [x] IDT setup
- [x] Paging
- [x] Disk I/O
- [x] XDVFS mount
- [x] Kernel loading

## License

Copyright © 2026 Dust LLC
