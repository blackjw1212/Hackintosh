# Changelog

## 2026-06-04 second-fix implementation

### Backup

- Created second-fix backup:
  `F:\Hackintosh-Ventura-Project\backups\EFI_20260604_103127_pre_second_fix`
- Exported second-fix pre-change snapshots:
  `F:\Hackintosh-Ventura-Project\Config-pre-second-fix-20260604_103127.plist`
  `F:\Hackintosh-Ventura-Project\UTBMap-pre-second-fix-20260604_103127.plist`

### USB / Bluetooth

- Updated `F:\EFI\OC\Kexts\UTBMap.kext\Contents\Info.plist`.
- Changed UTBMap `model` from `iMacPro1,1` to `iMac19,1`.
- Rebuilt the UTBMap port list to exactly 15 ports:
  `HS01, HS02, HS03, HS04, HS05, HS06, HS09, HS10, HS12, SS01, SS02, SS03, SS04, SS05, SS07`.
- Added `HS12` with `UsbConnector=255` and port data `0C000000` for Broadcom BT `13d3:3404`.
- Removed stale `HS07`, `HS08`, and `SS06` from the active map to stay within the 15-port limit.

### Picker

- Changed `Misc -> Boot -> PickerMode` to `Builtin`.
- Disabled `UEFI -> Drivers -> OpenCanopy.efi` because `F:\EFI\OC\Resources` is empty.
- Kept `OpenCanopy.efi` on disk as a future option if matching Resources are installed.

### Comments / maintenance

- Replaced stale NootRX route comments in `SSDT-BRG0.aml` and `SMCRadeonSensors.kext` comments.
- Updated implemented snapshots:
  `Config-Ventura-13.7.8-implemented.plist`
  `UTBMap-Ventura-13.7.8-implemented.plist`

## 2026-06-04 Ventura 13.7.8 implementation

### Backup

- Created original EFI backup:
  `F:\Hackintosh-Ventura-Project\backups\EFI_20260604_095417`
- Exported pre-edit config:
  `F:\Hackintosh-Ventura-Project\Config-pre-edit.plist`
- Note: `Config-pre-edit.plist` preserves the source file LastWriteTime `2026-04-21 20:10:38`.

### Config.plist

- Added RX 6650 XT DeviceProperties path:
  `PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)`.
- Added RX spoof property `device-id = FF730000`.
- Disabled `NootRX.kext`.
- Kept `WhateverGreen.kext` enabled.
- Changed `boot-args` to:
  `-v alcid=1 agdpmod=pikera brcmfx-driver=2`.
- Added Bluetooth NVRAM values:
  `bluetoothExternalDongleFailed = 00`
  `bluetoothInternalControllerInfo = 0000000000000000000000000000`.
- Added both Bluetooth keys to `NVRAM -> Delete`.
- Added `BrcmFirmwareData.kext` and `BrcmPatchRAM3.kext` to `Kernel -> Add`.
- Set `AirPortBrcm4360_Injector.kext` `MaxKernel` to `19.9.9`.
- Kept `AirPortBrcmNIC_Injector.kext` enabled with `MinKernel=21.0.0`.
- Corrected comments for ALC887 and Intel I219-V.

### Files added

- `F:\EFI\OC\Kexts\BrcmFirmwareData.kext`
- `F:\EFI\OC\Kexts\BrcmPatchRAM3.kext`

### Fallback retained

- `F:\EFI\OC\Kexts\NootRX.kext` remains present but disabled.
