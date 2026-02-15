# XDV-Boot - XDV Boot Loader

Version: 0.3.0
Status: Active
Language: Dust Programming Language (DPL)

## Overview

`xdv-boot` is the boot subsystem for XDV OS and models both startup paths:

- BIOS/MBR boot flow.
- UEFI/GPT boot flow.

The image pipeline in `xdv-os/src` consumes this layout to build 64MB partitioned artifacts.

## Source Layout

- `src/boot_mbr.ds` - MBR stage and partition-relative kernel load policy.
- `src/boot_uefi.ds` - UEFI stage and GPT/ESP flow model.
- `src/boot_stage1.ds` - shared stage sequencing.
- `src/boot_disk.ds` - disk access model.
- `src/boot_gdt.ds` - GDT setup model.
- `src/boot_idt.ds` - IDT setup model.
- `src/boot_paging.ds` - paging model.
- `src/boot_xdvfs_mount.ds` - xdvfs offsets and mount model.
- `src/boot_kernel_load.ds` - kernel load and handoff model.

## Build Check

```bash
dust check xdv-boot/src
```

## Notes

- BIOS stage machine code is assembled from `xdv-os/src/boot_sector.asm`.
- Partitioned image generation is implemented in `xdv-os/src/build_images.ps1`.
