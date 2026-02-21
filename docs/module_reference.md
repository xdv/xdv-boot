# Module Reference

## Core boot control

- `src/boot.ds`
  - Canonical `boot.bin` control path.
  - Coordinates splash, wait, firmware mode detection, kernel load, and handoff.

- `src/boot_loader_profile.ds`
  - Firmware-origin profile selection (`MBR` or `UEFI`).
  - Fallback profile behavior when mode is unknown.

## Kernel lookup and loading

- `src/boot_xdvfs_mount.ds`
  - xdvfs constants and mount validation.
  - Directory/path model for `/console/kernel.bin`.
  - Exports `xdvfs_get_console_kernel_lba()`.

- `src/boot_kernel_load.ds`
  - Kernel header read, format validation checks, segment load window, and entry jump support.

## Firmware-specific modules

- `src/boot_mbr.ds`
  - MBR signature validation and partition scan policy.
  - Partition-relative stage2/kernel helper routines.

- `src/boot_uefi.ds`
  - GPT validation and ESP mount profile.
  - UEFI-side kernel load and handoff helpers.

## Platform setup and disk model

- `src/boot_stage1.ds`
  - Stage init sequence model (stack, display, memory, CPU, disk, GDT, IDT, paging).

- `src/boot_disk.ds`
  - Disk-controller modeling, LBA/buffer checks, read/write/identify behavior.

- `src/boot_gdt.ds`
  - GDT descriptor setup model.

- `src/boot_idt.ds`
  - IDT and exception vector setup model.

- `src/boot_paging.ds`
  - Paging structure and activation model.

## Test modules

- `src/boot_disk_tests.ds`
- `src/boot_gdt_tests.ds`
- `src/boot_idt_tests.ds`
- `src/boot_kernel_load_tests.ds`
- `src/boot_mbr_tests.ds`
- `src/boot_paging_tests.ds`
- `src/boot_stage1_tests.ds`
- `src/boot_uefi_tests.ds`
- `src/boot_xdvfs_mount_tests.ds`

These files provide module-level verification for the boot pipeline components.
