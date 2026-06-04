# Validation Report

Date: 2026-06-04

## Scope

This report covers Windows-side offline mechanical validation only. It does not mean Ventura real-machine validation is complete.

Not completed yet:

- Matching OpenCore `ocvalidate`.
- macOS `system_profiler`, `kmutil`, IORegistryExplorer, Hackintool, or `gfxutil`.
- Cold boot, reboot, sleep/wake, USB, Bluetooth, Wi-Fi, audio, Ethernet, and GPU real-machine tests.

## Offline Mechanical Validation Passed

- `F:\EFI\OC\Config.plist` parses successfully.
- `F:\EFI\OC\Kexts\UTBMap.kext\Contents\Info.plist` parses successfully.
- SMBIOS remains `iMac19,1`.
- UTBMap `model=iMac19,1`, matching SMBIOS.
- UTBMap has exactly 15 ports:
  `HS01, HS02, HS03, HS04, HS05, HS06, HS09, HS10, HS12, SS01, SS02, SS03, SS04, SS05, SS07`.
- `HS12` is present with `UsbConnector=255` and port data `0C000000`.
- `PickerMode=Builtin`.
- `OpenCanopy.efi` is disabled because `EFI\OC\Resources` is empty.
- Enabled ACPI, Drivers, Tools, and Kext entries all reference existing files.
- Enabled kexts have `Contents/Info.plist`; executable kext entries have their executable path present.
- Kext order checks pass:
  `Lilu` before Lilu plugins.
  `VirtualSMC` before SMC sensors.
  `USBToolBox` before `UTBMap`.
  `BrcmFirmwareData` before `BrcmPatchRAM3`.
- `NootRX.kext` is disabled.
- `BrcmBluetoothInjector.kext` is not enabled.
- Bluetooth NVRAM Add/Delete keys are present.

Result: `0 errors, 0 warnings`.

## Boot-Critical Notes

- RX 6650 XT Windows LocationPaths:
  `PCIROOT(0)#PCI(0100)#PCI(0000)#PCI(0000)#PCI(0000)`
- Converted OpenCore path:
  `PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)`
- USB BT was observed on root USB port 12; UTBMap now includes `HS12` as Internal.
- If the first Ventura boot fails, use `RECOVERY.md` and the second-fix backup first.

## Known Residual Risk

- USB map is improved from observed Windows device locations, but every physical port still needs macOS testing.
- HS09 and HS10 were kept because Windows showed present USB HID devices there.
- HS07, HS08, and SS06 were removed to keep the 15-port limit. Retest physical USB coverage and remap if any removed port is required.
- `Config-pre-edit.plist` intentionally preserves original LastWriteTime `2026-04-21 20:10:38`.
