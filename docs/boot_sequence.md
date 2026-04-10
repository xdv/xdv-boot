# Boot Sequence

`xdv-boot/src/boot.ds` defines the canonical `boot.bin` sequence:

1. `boot_render_splash_step()`
2. `boot_wait_splash_window()`
3. `boot_probe_firmware_origin()`
4. `boot_verify_firmware_path(mode)`
5. `boot_locate_and_load_kernel(mode)`
6. `boot_kernel_handoff()`

## Detailed Flow

## 1) Splash render

- Module: `src/boot_splash_profile.ds`
- Entry: `boot_splash_contract()`
- Behavior: emits the XDV ASCII splash lines.

## 2) Splash hold window (8 seconds)

- Module: `src/boot.ds`
- Entry: `boot_wait_splash_window()`
- Behavior: delegates timing behavior to `xdv_boot_prepare(8)` in xdv-lib runtime support.

## 3) Firmware-origin recognition

- Module: `src/boot_loader_profile.ds`
- Entry: `boot_loader_detect_mode(depth)`
- Behavior:
  - attempts MBR profile (`mbr_init()`),
  - attempts UEFI profile (`uefi_stage_init()`),
  - returns unknown only when both fail.

## 4) MBR/UEFI parity validation

- Module: `src/boot.ds`
- Entry: `boot_verify_firmware_path(mode)`
- Behavior:
  - if mode is MBR, re-validates MBR profile path,
  - if mode is UEFI, re-validates UEFI profile path,
  - aborts boot on parity mismatch.

## 5) Kernel location and load

- Module: `src/boot_xdvfs_mount.ds`
  - `xdvfs_mount_device(device)`
  - `xdvfs_get_console_kernel_lba()`
- Module: `src/boot_kernel_load.ds`
  - `kernel_load_from_lba(kernel_lba)`
  - `kernel_validate_elf()`
  - `kernel_load_segments(kernel_lba)`

Kernel lookup target is:

- `xdvfs:/console/kernel.bin`

## 6) Strict handoff

- Module: `src/boot.ds`
- Entry: `boot_kernel_handoff()`
- Behavior:
  - requires `kernel_get_entry() > 0`,
  - requires `kernel_jump_to_entry()` strict precheck success,
  - calls `xdv_boot_transfer_kernel()` only after precheck success.

Assembly-side transfer additionally rejects zero/out-of-window entry offsets before jump.

## Failure-path logs

`boot.ds`, `boot_mbr.ds`, `boot_uefi.ds`, and `boot_kernel_load.ds` emit explicit
`xdv-boot: failure: ...` logs for contract failures.

## Integration Contract with xdv-os

- Stage0 in `xdv-os/src/boot_sector.asm` must load `boot.bin` only.
- `boot.bin` owns kernel discovery and transfer.
- xdv-os image build must preload `kernel.bin` at `/console/kernel.bin` on xdvfs.