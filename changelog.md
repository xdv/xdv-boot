# XDV-Boot Changelog

## 2026-02-20

### Added

- Added documentation set under `xdv-boot/docs/`:
  - `docs/README.md`
  - `docs/boot_sequence.md`
  - `docs/module_reference.md`
- Added this changelog file.

### Changed

- Updated `README.md` to reflect current canonical `boot.bin` contract:
  - stage0 loads `boot.bin` only,
  - splash + 8-second hold path,
  - firmware-origin recognition (MBR/UEFI),
  - xdvfs kernel lookup at `/console/kernel.bin`,
  - boot-side kernel handoff.

## 2026-02-19

### Changed

- Boot flow was formalized in `src/boot.ds` as:
  - splash -> wait -> firmware-origin detection -> `/console/kernel.bin` load -> handoff.
- Kernel lookup path was aligned to xdvfs `/console/kernel.bin` via `src/boot_xdvfs_mount.ds`.
- Kernel loader messages and semantics were updated in `src/boot_kernel_load.ds`, `src/boot_mbr.ds`, and `src/boot_uefi.ds` to follow the console kernel path.
