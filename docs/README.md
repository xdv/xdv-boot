# XDV-Boot Documentation

This directory documents `xdv-boot` as the `boot.bin` runtime used by XDV OS.

## Documents

- `boot_sequence.md`: end-to-end execution path from stage0 handoff through kernel transfer.
- `module_reference.md`: source file responsibilities and key procedures.

## Scope

`xdv-boot` is responsible for:

- splash presentation and splash hold window,
- recognizing firmware origin (MBR vs UEFI),
- mounting xdvfs and locating `/console/kernel.bin`,
- loading and transferring control to kernel entry.

`xdv-boot` is not responsible for stage0 sector bootstrap assembly in `xdv-os/src/boot_sector.asm`.
