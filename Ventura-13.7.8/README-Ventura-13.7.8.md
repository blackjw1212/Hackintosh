# Ventura 13.7.8 EFI Project

Target OS: macOS Ventura 13.7.8

Status: offline implementation complete; offline mechanical validation passed. Matching OpenCore `ocvalidate` and real-machine macOS boot tests are still required.

## Summary

Ventura 13.7.8 is the recommended mainline for this Coffee Lake / Z370 / RX 6650 XT build. Monterey 12.7.6 can also run on this platform, but Ventura has the better security and app-compatibility runway.

## Hardware Matrix

| Area | Detected hardware | Ventura route |
| --- | --- | --- |
| CPU | Intel Core i7-9700 | Coffee Lake, SMBIOS `iMac19,1` |
| Board | ASUS TUF Z370-PLUS GAMING, BIOS 3004 | Z370 with EC/USBX/AWAC/PLUG style ACPI |
| GPU | AMD RX 6650 XT `1002:73EF` | `WhateverGreen` + spoof to `73FF` |
| iGPU | Intel UHD 630 | Headless injection; BIOS iGPU must be enabled |
| Audio | Realtek ALC887 | `AppleALC` + `alcid=1` |
| Ethernet | Intel I219-V `8086:15B8` | `IntelMausi` |
| Wi-Fi | Broadcom `14e4:43b1` | `AirportBrcmFixup` + `AirPortBrcmNIC_Injector` |
| Bluetooth | USB `13d3:3404` | `BlueToolFixup` + `BrcmFirmwareData` + `BrcmPatchRAM3` |
| USB | USBToolBox + UTBMap | BT root port 12 mapped as internal `HS12` |

## Implemented In Live EFI

- SMBIOS remains `iMac19,1`; Serial, MLB, SystemUUID, and ROM were not changed.
- RX 6650 XT uses `WhateverGreen.kext` with DeviceProperties `device-id = FF730000`.
- `NootRX.kext` is present but disabled as a fallback.
- `boot-args`: `-v alcid=1 agdpmod=pikera brcmfx-driver=2`.
- Broadcom BT kext set: `BlueToolFixup.kext`, `BrcmFirmwareData.kext`, `BrcmPatchRAM3.kext`.
- Bluetooth NVRAM keys were added:
  `bluetoothExternalDongleFailed=00`
  `bluetoothInternalControllerInfo=0000000000000000000000000000`
- UTBMap now has `model=iMac19,1`, exactly 15 ports, and `HS12` marked Internal.
- `PickerMode=Builtin`; `OpenCanopy.efi` is disabled because `EFI\OC\Resources` is empty.

## Key Artifacts

- Live EFI: `F:\EFI`
- Original backup: `F:\Hackintosh-Ventura-Project\backups\EFI_20260604_095417`
- Second-fix backup: `F:\Hackintosh-Ventura-Project\backups\EFI_20260604_103127_pre_second_fix`
- Implemented config: `F:\Hackintosh-Ventura-Project\Config-Ventura-13.7.8-implemented.plist`
- Implemented UTBMap: `F:\Hackintosh-Ventura-Project\UTBMap-Ventura-13.7.8-implemented.plist`
- Latest EFI zip: use `EFI-post-second-fix-*`.
- Complete manifest: use `SHA256-complete-*`.

## Next Gate

Run Reset NVRAM from the OpenCore picker, then perform the test plan in `BOOT-TEST.md`. If the first boot fails, use `RECOVERY.md`.
