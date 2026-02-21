# XDV-Boot

Status: Active  
Language: Dust Programming Language (DPL)

`xdv-boot` is the `boot.bin` runtime for XDV OS.

It owns the boot sequence after stage0 loads `boot.bin`:

1. render XDV splash,
2. hold splash window for 8 seconds,
3. detect firmware origin (MBR or UEFI),
4. mount xdvfs and resolve `/console/kernel.bin`,
5. load kernel image and hand off execution.

## Boot Contract

- Stage0 (`xdv-os/src/boot_sector.asm`) loads `boot.bin` only.
- `xdv-boot` resolves kernel location from xdvfs (`/console/kernel.bin`).
- `xdv-boot` performs final transfer to kernel entry.

## Repository Layout

- `src/boot.ds`: canonical boot flow for `boot.bin`.
- `src/boot_splash_profile.ds`: ASCII splash payload.
- `src/boot_loader_profile.ds`: MBR/UEFI origin recognition.
- `src/boot_mbr.ds`: MBR partition profile and load helpers.
- `src/boot_uefi.ds`: UEFI/GPT profile and kernel handoff helpers.
- `src/boot_xdvfs_mount.ds`: xdvfs mount and `/console/kernel.bin` lookup.
- `src/boot_kernel_load.ds`: kernel header read, validation, segment load, entry jump.
- `src/boot_stage1.ds`: stage init orchestration model.
- `src/boot_disk.ds`: disk access and read/write checks.
- `src/boot_gdt.ds`, `src/boot_idt.ds`, `src/boot_paging.ds`: boot CPU/runtime setup models.
- `src/*_tests.ds`: module-level behavior tests.

## Documentation

- `docs/README.md`
- `docs/boot_sequence.md`
- `docs/module_reference.md`
- `changelog.md`

## Validate

```bash
dust check xdv-boot/src
```
