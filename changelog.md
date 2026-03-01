# XDV-Boot Changelog

## 2026-02-28

### Changed

- Finalized canonical boot sequence in `src/boot.ds`:
  - splash render,
  - 8-second splash timer window,
  - firmware-origin detection,
  - MBR/UEFI parity verification,
  - `/console/kernel.bin` load,
  - strict handoff precheck + transfer.
- Added explicit boot failure-path logging (`xdv-boot: failure: ...`) across:
  - `src/boot.ds`
  - `src/boot_mbr.ds`
  - `src/boot_uefi.ds`
  - `src/boot_kernel_load.ds`
- Tightened strict handoff semantics:
  - `boot.ds` now requires valid entry precheck before transfer,
  - `xdv-lib` boot wrapper now propagates transfer status,
  - `xdv_lib_boot_runtime.asm` now rejects zero/out-of-window entry offsets.
- Replaced placeholder MBR/UEFI tests with parity/failure-path test cases in:
  - `src/boot_mbr_tests.ds`
  - `src/boot_uefi_tests.ds`
- Updated README and docs for XDV-062 flow and strict handoff behavior.

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