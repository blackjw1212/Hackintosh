# Release Status

Updated: 2026-06-04

## Current State

Status: offline implementation complete, offline mechanical validation passed.

Not yet complete:

- Matching OpenCore `ocvalidate`.
- Ventura 13.7.8 real-machine boot test.
- macOS hardware verification for GPU, Quick Sync, USB, Bluetooth, Wi-Fi, audio, Ethernet, sleep/wake.

## Fixed In Second Pass

- P1 USB/BT issue addressed: UTBMap now includes `HS12` as Internal for Broadcom BT `13d3:3404`.
- UTBMap model now matches SMBIOS `iMac19,1`.
- OpenCanopy empty Resources risk addressed: `PickerMode=Builtin`, `OpenCanopy.efi` disabled.
- Stale NootRX comments cleaned.
- Recovery docs no longer assume `F:\EFI` is always the mounted ESP.

## Current Live EFI Highlights

- `NootRX.kext`: present but disabled.
- `WhateverGreen.kext`: enabled.
- RX spoof: `device-id=FF730000`.
- `boot-args`: `-v alcid=1 agdpmod=pikera brcmfx-driver=2`.
- Broadcom BT: `BlueToolFixup + BrcmFirmwareData + BrcmPatchRAM3`.
- USB map ports:
  `HS01, HS02, HS03, HS04, HS05, HS06, HS09, HS10, HS12, SS01, SS02, SS03, SS04, SS05, SS07`.
- Picker: Builtin.

## Delivered Artifacts

- Live EFI: `F:\EFI`
- Original backup: `F:\Hackintosh-Ventura-Project\backups\EFI_20260604_095417`
- Second-fix backup: `F:\Hackintosh-Ventura-Project\backups\EFI_20260604_103127_pre_second_fix`
- Implemented config: `F:\Hackintosh-Ventura-Project\Config-Ventura-13.7.8-implemented.plist`
- Implemented UTBMap: `F:\Hackintosh-Ventura-Project\UTBMap-Ventura-13.7.8-implemented.plist`
- Latest EFI zip: `F:\Hackintosh-Ventura-Project\EFI-post-second-fix-20260604_103654.zip`
- Complete manifest: use the latest `F:\Hackintosh-Ventura-Project\SHA256-complete-*.txt`.

## Required Next Gate

Before calling this production-ready, complete:

1. Matching OpenCore `ocvalidate`.
2. Reset NVRAM.
3. First boot into Ventura 13.7.8.
4. Run `BOOT-TEST.md`.
5. Record System Information / IORegistry evidence for RX 6650 XT spoof, HS12 Bluetooth, Wi-Fi, audio, Ethernet, and sleep/wake.
