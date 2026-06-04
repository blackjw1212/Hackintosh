# EFI Inventory

## OpenCore

- `OpenCore.efi` present at `F:\EFI\OC\OpenCore.efi`.
- Matching `ocvalidate.exe` was not found in `F:\EFI` or the project folder.
- OpenCore binary version was not reliably extracted, so no cross-version `ocvalidate` was run.

## Enabled ACPI

- `ssdt_data.aml`
- `SSDT-EC-USBX.aml`
- `SSDT-AWAC.aml`

## Drivers

Enabled:

- `HfsPlus.efi`
- `OpenRuntime.efi`
- `ResetNvramEntry.efi`
- `ToggleSipEntry.efi`

Disabled:

- `OpenCanopy.efi` because Resources are empty.
- `OpenHfsPlus.efi` because `HfsPlus.efi` is already enabled.

## Key Kexts

| Kext | Version | Status | Purpose |
| --- | --- | --- | --- |
| Lilu.kext | 1.7.2 | Enabled | Plugin base |
| VirtualSMC.kext | 1.3.7 | Enabled | SMC emulation |
| WhateverGreen.kext | 1.7.0 | Enabled | UHD 630 headless + RX 6650 XT spoof |
| NootRX.kext | 1.0.0 | Disabled | Fallback only |
| AppleALC.kext | 1.9.7 | Enabled | ALC887 audio |
| IntelMausi.kext | 1.0.8 | Enabled | Intel I219-V Ethernet |
| NVMeFix.kext | 1.1.3 | Enabled | NVMe fixes |
| AirportBrcmFixup.kext | 2.2.0 | Enabled | Broadcom Wi-Fi |
| BlueToolFixup.kext | 2.7.2 | Enabled | macOS 12+ Bluetooth stack fix |
| BrcmFirmwareData.kext | 2.7.2 | Enabled | Broadcom firmware store |
| BrcmPatchRAM3.kext | 2.7.2 | Enabled | Broadcom firmware uploader |
| USBToolBox.kext | 1.2.0 | Enabled | USB map provider |
| UTBMap.kext | 1.1.1 | Enabled | USB port map |

## UTBMap

- Personality: `XHC`
- Model: `iMac19,1`
- Port count: 15
- Ports:
  `HS01, HS02, HS03, HS04, HS05, HS06, HS09, HS10, HS12, SS01, SS02, SS03, SS04, SS05, SS07`
- `HS12` is Internal for Broadcom BT `13d3:3404`.

## Disabled But Present

- `CPUFriend.kext`
- `CPUFriendDataProvider.kext`
- `USBPorts.kext`
- `NootRX.kext`
